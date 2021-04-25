<script>
	import Main from './components/main.svelte';
	import Header from './components/header.svelte';
	let selectedCountry = '';
	// this handles the forwarded event (on:country)
	function getDataForCountry(event) {
		selectedCountry = event.details.country;
	}

	let loading = true;
    let title = 'Global';
    let dataDate = '';
    let stats = {};
    let countries = [];
	let data;

	function updateProps(data) {
		if (!data) {
			return;
		}
		loading = false;
		countries = data.Countries;
		stats = data.Global;
		dataDate = data.Date;
	}
	async function fetchCovidData() {
		let res = await fetch('https://api.covid19api.com/summary');
		if (res.ok) {
			data = await res.json();
			updateProps(data);
			return data;
		} else {
			throw Error(res.json())
		}
    }
	
	fetchCovidData();
</script>

<style global lang="postcss">
	@tailwind base;
	@tailwind components;

	/* purgecss end ignore */
  	@tailwind utilities;
	@layer utilities {
		.ml-55 {
			margin-left: 55%;
		}
	}
</style>

<Header />
<Main on:country={getDataForCountry} 
		loading={loading}
		title={title}
		countries={countries}
		stats={stats}
		dataDate={dataDate}
		selectedCountry={selectedCountry}
/>
