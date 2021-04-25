<script>
	import Main from './components/main.svelte';
	import Header from './components/header.svelte';
	import Footer from './components/footer.svelte';

	let selectedCountry = '';
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
		title = 'Global'; // by default, it is for global
		selectedCountry = ''; // since it is global data
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

	// this handles the forwarded event (on:country)
	function getDataForCountry(event) {
		selectedCountry = event.detail.country;
		let countryObj = countries.find((obj) => obj.CountryCode === selectedCountry)
		stats = countryObj;
		title = countryObj.Country;
	}

	function resetGlobal(event) {
		fetchCovidData(); // it will load the global status
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
<div class='container flex flex-col items-center max-w-md md:w-full'>
	<Header />
	<Main on:country={getDataForCountry} on:clearCountry={resetGlobal}
		loading={loading}
		title={title}
		countries={countries}
		stats={stats}
		dataDate={dataDate}
		selectedCountry={selectedCountry}
	/>
	<Footer />
</div>
