<script>
    import TranslationMenu from './TranslationMenu.svelte'
    import MaterialIcon from './MaterialIcon.svelte'

    let innerWidth
    let opened = false;

</script>

<svelte:window bind:innerWidth={innerWidth}/>

<header>
    {#if innerWidth > 768}
        <div class="header-bar">
            <h3 class="title is-3" id="title">Who's Open Uptown Grand Central</h3>
            <div class="buttons has-text-right">
                <TranslationMenu className="is-small"/>
                <button class="button is-small {opened ? 'is-clicked' : ''}" on:click={() => opened = !opened}>
                    <MaterialIcon icon="info"></MaterialIcon>
                </button>
            </div>
        </div>
        {#if opened}
            <div id="subtitle">
                <p class="is-6 subtitle"><strong>Businesses in Uptown Grand Central</strong>
                    <br/><br/>Please call ahead or check website/social media before you visit
                    for the most current information.</p>
                <p class="is-6 subtitle">Maintained by <a href="http://uptowngrandcentral.org" target="_blank">Uptown
                    Grand Central</a>. To add or update info fill out <a href="https://airtable.com/shrbLNyrAUlnk45R7"
                                                                         target="_blank">this form</a>.</p>
            </div>
        {/if}
    {:else}
        <div class="header-bar">
            <h3 class="title is-5">Who's Open Uptown Grand Central</h3>
            <div class="buttons has-text-right">
                <TranslationMenu className="is-small"/>
                <button class="button is-small {opened ? 'is-clicked' : ''}" on:click={() => opened = !opened}>
                    <MaterialIcon icon="info"></MaterialIcon>
                </button>
            </div>
        </div>
        {#if opened}
            <div id="subtitle">
                <p class="is-6 subtitle"><strong>Businesses in Uptown Grand Central</strong>
                    <br/><br/>Please call ahead or check website/social media before you visit
                    for the most current information.</p>
                <p class="is-6 subtitle">Maintained by <a href="http://uptowngrandcentral.org" target="_blank">Uptown
                    Grand Central</a>. To add or update info fill out <a href="https://airtable.com/shrbLNyrAUlnk45R7"
                                                                         target="_blank">this form</a>.</p>
            </div>
        {/if}
    {/if}
</header>

<style>
    .header-bar {
        margin: 1rem 0rem;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    .title {
        margin-bottom: 10px !important;
    }

    .has-background-warning {
        padding: 0.2rem 1rem;
    }

    @media only screen and (max-width: 768px) {

        #subtitle {
            margin-top: 5px;
            background-color: #eaeaea;
            padding: 1rem 2rem;
            z-index: 2;
        }
    }

    .is-clicked {
        background-color: #ecf1f8;
    }

    p {
        margin-bottom: 0.25rem !important;
    }
</style>