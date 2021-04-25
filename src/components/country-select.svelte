 <script>
  import { createEventDispatcher } from 'svelte';
  let dispatcher = createEventDispatcher();
  
  function handleSelection(event) {
    dispatcher('country', {
      country: selectedCountry
    });
  }

  // props from parent
  export let selectedCountry;
  export let countries;
 </script>
 
<select bind:value={selectedCountry} on:change={ handleSelection }
  class="form-select mt-10 block w-full border p-3 rounded">
  <option value="">Select Country</option>
  {#each countries as country}
    <option value={country.CountryCode}>{country.Country}</option>
  {/each}
</select>
