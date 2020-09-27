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
                <a>
                    <MaterialIcon icon="list" alt="List of business"/>
                </a>
            </li>
            <li class="nav-item" on:click={() => navSelected = 'filters'}>
                <a>
                    <MaterialIcon icon="filter_alt" alt="More Filters"/>
                </a>
            </li>
        </ul>

    </nav>
    <div class="sidebar-content">
        {#if $selectedItem}
            <ItemDetails hidden={!$selectedItem}/>
        {:else}
            <div class="search">
                <AddressSearch/>
                <NameSearch/>
                <OtherFilters hidden={navSelected !== 'filters'}/>
            </div>
            <div class="items {navSelected !== 'list' ? 'is-hidden' : ''}">
                <RowItems {items} show={!$selectedItem}/>
            </div>
        {/if}
    </div>
</div>

<style>
    .sidebar {
        display: flex;
        height: 100%
    }

    .nav-items {
        list-style: none;
        margin-left: 0;
        margin-right: 5px;
        display: flex;
        flex-direction: column;
        align-content: space-between;
        width: 40px;
    }

    .nav-item {
        height: 4rem;
        background-color: #eef7ff;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .nav-item:hover {
        background-color: #a3bae5;
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

    .items {
        margin-top: 1rem;
        flex: 1 1 80%;
        overflow: auto;
        position: relative;
        box-shadow: 0px 0px 2px 2px rgba(128, 128, 128, 0.2);
    }

</style>