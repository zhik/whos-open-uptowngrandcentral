<script>
    import {selectedItem} from '../stores'
    import NameSearch from './sidebar/filters/NameSearch.svelte'
    import RowItems from './sidebar/RowItems.svelte'
    import ItemDetails from './sidebar/details/ItemDetails.svelte'
    import OtherFilters from './sidebar/filters/OtherFilters.svelte'
    import AddressSearch from './sidebar/AddressSearch.svelte'
    import MaterialIcon from './MaterialIcon.svelte'

    export let items = []
    let navSelected = 'list'
</script>

<div class="sidebar">
    <nav class="sidebar-nav">
        <ul class="nav-items">
            <li class="nav-item" on:click={() => navSelected = 'list'}>
                <a class="{navSelected === 'list' ? 'selected' : ''}">
                    <MaterialIcon icon="list" alt="List of business"/>
                </a>
            </li>
            <li class="nav-item" on:click={() => navSelected = 'filters'}>
                <a class="{navSelected === 'filters' ? 'selected' : ''}">
                    <MaterialIcon icon="filter_alt" alt="More Filters"/>
                </a>
            </li>
        </ul>

    </nav>
    <div class="sidebar-content">
        <div class="details {!$selectedItem ? 'is-hidden' : ''}">
            <ItemDetails/>
        </div>
        <div class="search {$selectedItem ? 'is-hidden' : ''}">
            <AddressSearch/>
            <NameSearch hidden={navSelected === 'filters'}/>
            <OtherFilters hidden={navSelected !== 'filters'}/>
        </div>
        <div class="items {navSelected !== 'list' || $selectedItem ? 'is-hidden' : ''}">
            <RowItems {items} show={!$selectedItem}/>
        </div>
    </div>
</div>

<style>
    .sidebar {
        display: flex;
        height: 100%
    }

    .nav-items {
        list-style: none;
        margin: 0 5px 0 0;
        display: flex;
        flex-direction: column;
        align-content: space-between;
        width: 40px;
        background-color: #D6DEE5;
    }

    .nav-item {
        margin: 1px;
        height: 6rem;
    }

    .nav-item a{
        height: 100%;
        width: 100%;
        background-color: #eef7ff;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .nav-item a:hover {
        background-color: #b5c0f8;
    }

    .nav-item a.selected{
        background-color: #c0ced7;
        border: rgba(90, 115, 236, 0.8) 1px solid;
    }

    .nav-item a.selected span{
        color: grey;
    }

    .sidebar-content {
        display: flex;
        flex-direction: column;
        height: 100%;
        width: 100%;
    }

    .search {
        flex: 1 1 auto;
    }

    .items{
        margin-top: 1rem;
        flex: 1 1 80%;
        overflow: auto;
        position: relative;
        box-shadow: 0px 0px 2px 2px rgba(128, 128, 128, 0.2);
    }

    .details{
        flex: 1 1 80%;
        overflow: auto;
        position: relative;
    }

    .items.is-hidden {
        display: none;
    }

</style>