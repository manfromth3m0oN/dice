<script>
	import axios from "axios";
	import {onMount} from "svelte";
	let rawData;
	let roll = 0;
	let rolled;
	let col1roll;
	let col2roll;
	let dataUrl = 'https://raw.githubusercontent.com/manfromth3m0oN/dice/master/test.json'
	onMount(async () => {
		getJson().then(data => {
			rawData = data
		})
	})

	function getJson() {
		return axios.get(dataUrl)
			.then((response) => {
				console.log(response.data)
				return response.data
			})
	};

	function getRndInteger(max) {
		return Math.floor(Math.random() * (max - 0 + 1) ) + 0;
	};

	function rollDie() {
		if (Object.keys(rawData).length == 2) {
			col1roll = getRndInteger(rawData['col1'].length - 1)
			col2roll = getRndInteger(rawData['col2'].length - 1)
		} else if (Object.keys(rawData).length == 1) {
			coll1roll = getRndInteger(rawData['col1'].length)
		}
		rolled = true
	};
	function clear() {
		col1roll = -1;
		col2roll = -1;
	}
</script>

<main>
	<button on:click={rollDie}>Roll the dice</button><br/>
	{#if col1roll >= 0}
		<p>Column 1:</p>{rawData['col1'][col1roll]}
	{/if}

	{#if col2roll >= 0}
		<p>Column 2:</p>{rawData['col2'][col2roll]}
	{/if} <br/>
	<button on:click={clear}>Clear the results</button>
</main>

<style>

</style>