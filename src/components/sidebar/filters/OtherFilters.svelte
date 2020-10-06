<script>
    import CategoryFilters from './CategoryFilters.svelte'
    import OpenedFilter from './OpenedFilter.svelte'
    import PickupDeliveryFilter from './PickupDeliveryFilter.svelte'
    import MaterialIcon from '../../MaterialIcon.svelte'
    import OwnedByFilters from './OwnedByFilters.svelte'
    import OutdoorSeating from './OutdoorSeating.svelte'
    import IndoorSeating from './IndoorSeating.svelte'

    export let hidden = false
    let opened = false
</script>

<div class="filters {hidden ? 'is-hidden' : ''}" >
    <OutdoorSeating/>
    <IndoorSeating/>
    <br/>
    <CategoryFilters/>
    <button class="full" on:click={() => opened = !opened}>
        <p style="margin-left: -1.2rem;">
            <MaterialIcon size="small" icon="{opened? 'expand_less' : 'expand_more'}"/> More Filters
        </p>
    </button>
    <div class={opened ? '' : 'is-hidden'}>
        <div class="field">
            <label class="label">Businesses owned by</label>
            <OwnedByFilters name="Minority and/or women-owned " column="MWBE"/>
            <OwnedByFilters name="Black-owned" column="Black Owned Business"/>
        </div>
        <OpenedFilter/>
        <PickupDeliveryFilter/>
    </div>
</div>

<style>
    .full {
        display: block;
        width: 100%;
        border: solid 1px #d5d5d5;
        border-radius: 4px;
        padding: 2px 7px;
        font-size: 0.7rem;
    }
    
    br{
        margin-top: 0;
        margin-bottom: 10px;
    }
</style>