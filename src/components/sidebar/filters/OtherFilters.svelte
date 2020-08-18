<script>
    import CategoryFilters from './CategoryFilters.svelte'
    import OpenedFilter from './OpenedFilter.svelte'
    import PickupDeliveryFilter from './PickupDeliveryFilter.svelte'
    import MaterialIcon from '../../MaterialIcon.svelte'
    import OwnedByFilters from './OwnedByFilters.svelte'
    import OutdoorSeating from './OutdoorSeating.svelte'

    let opened = false

</script>
<OutdoorSeating/>
<CategoryFilters/>
<button class="full" on:click={() => opened = !opened}>
    More Filters <MaterialIcon size="small" icon="{opened? 'expand_less' : 'expand_more'}"/>
</button>
<div class={opened ? '' : 'hidden'}>
    <div class="field">
        <label class="label">Businesses owned by</label>
        <OwnedByFilters name="Minority and/or women-owned " column="MWBE"/>
        <OwnedByFilters name="Black-owned" column="Black Owned Business"/>
    </div>
    <OpenedFilter/>
    <PickupDeliveryFilter/>
</div>

<style>
    .full {
        display: block;
        width: 100%;
        border: solid 1px #d5d5d5;
        border-radius: 4px;
        padding: 5px 10px;
    }

    .hidden{
        display: none;
    }
</style>