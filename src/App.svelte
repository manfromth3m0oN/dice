<script>
	import Papa from "papaparse";
	import {onMount} from "svelte";

	onMount(async () => {
		Papa.parse('https://raw.githubusercontent.com/manfromth3m0oN/dice/master/test.csv', {
			download: true,
			complete: function (results) {
				rawData = results.data;
				listLength = results.data.length;
			}
		})
		formatRawData();
	})

	let rawData;
	let roll = 0;
	let listLength;
	let result;
	let col1 = [];
	let col2 = [];
	let i;

	function getRndInteger() {
		roll = Math.floor(Math.random() * (listLength - 0 + 1) ) + 0;
	}

	function formatRawData() {
		for (i=0; i<listLength; i++) {
			col1.push(rawData[i][0]);
			col2.push(rawData[i][1]);
		}
	}


</script>

<main>
	The roll is {roll} <br/>
	<button on:click={getRndInteger}>Roll the dice</button><br/>
	{col1}
	{col2}
</main>

<style>

</style>