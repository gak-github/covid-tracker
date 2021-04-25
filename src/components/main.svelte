<script>
    import { createEventDispatcher } from 'svelte';
    import Title from './title.svelte';
    import Data from './data.svelte';
    import CountrySelect from './country-select.svelte';
    
    // props being passed from parent component
    export let loading;
    export let stats;
    export let dataDate;
    export let countries;
    export let title;
    export let selectedCountry;

    let dispatch = createEventDispatcher();
    function handleClick(event) {
        dispatch('clearCountry', {});
    }
</script>
{#if !loading}
    <main>
        <Title title={title} dataDate={dataDate} />
        <Data stats={stats} />
        <CountrySelect countries={countries} selectedCountry={selectedCountry} on:country />
        
        <button
            on:click={handleClick}
            class="bg-green-600 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
        >
            Clear Country
        </button>
    </main>
{:else}
    <main class="flex flex-col align-center justify-center text-center" v-else>
        <div class="text-gray-500 text-3lg mt-10 mb-6">
            Fetching Data
        </div>
        <span class="iconify w-24 m-auto" data-icon="icomoon-free:spinner3" data-inline="false" data-width="48" data-height="48" data-rotate="270deg" data-flip="horizontal"></span>
    </main>
{/if}