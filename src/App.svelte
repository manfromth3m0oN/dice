<script>
	import axios from "axios";
	import {onMount} from "svelte";
	export let title = 'deviants dice';
	$: document.title = title;
	let rawData;
	let roll = 0;
	let rolled;
	let col1roll;
	let col2roll;
	let dataUrl = 'https://raw.githubusercontent.com/manfromth3m0oN/dice/master/test.json';
	let options = [
		{ id: 1, text: "option 1" },
		{ id: 2, text: "option 2" },
		{ id: 3, text: "option 3" }
	];
	let selected;
	let answer = '';
	let left = ["body part", "action"];
	let right = ["action", "time"];
	let mode;

	onMount(async () => {
		getJson().then(data => {
			rawData = data
		})
		mode = 0
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
	};
	function reroll(col) {
		if (col == 1) {
			col1roll = getRndInteger(rawData['col1'].length - 1)
		}
		if (col == 2) {
			col2roll = getRndInteger(rawData['col2'].length - 1)
		}
	};
	function switchmode(desiredMode) {
		if (desiredMode == 0){
			mode = 0
		} else if (desiredMode == 1) {
			mode = 1
		}
	}
</script>

<button class="help">
	<svg width="47" height="47" viewBox="0 0 47 47" fill="none" xmlns="http://www.w3.org/2000/svg">
		<path d="M17.801 17.6249C18.7517 14.9225 21.5128 13.2998 24.3363 13.7841C27.1598 14.2684 29.2224 16.7185 29.2181 19.5833C29.2181 23.4999 23.3431 25.4583 23.3431 25.4583" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
		<path fill-rule="evenodd" clip-rule="evenodd" d="M23.5001 43.0834C34.3157 43.0834 43.0834 34.3157 43.0834 23.5001C43.0834 12.6845 34.3157 3.91675 23.5001 3.91675C12.6845 3.91675 3.91675 12.6845 3.91675 23.5001C3.91675 34.3157 12.6845 43.0834 23.5001 43.0834Z" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
		<circle cx="23.5001" cy="33.2916" r="1.95833" fill="white"/>
	</svg>
</button>

<main>
	<link href="https://fonts.googleapis.com/css2?family=Lato:wght@300&family=Lustria&display=swap" rel="stylesheet">

	<div class="container">
		<div class="modeButtons">
		<button on:click={() => switchmode(0)} class="modeButton">
				<svg width="100" height="100" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
					<circle cx="50" cy="50" r="50" fill="white"/>
					<path fill-rule="evenodd" clip-rule="evenodd" d="M72.1002 31.5249C69.5214 28.9449 66.023 27.4954 62.3752 27.4954C58.7273 27.4954 55.229 28.9449 52.6502 31.5249L50.0002 34.1749L47.3502 31.5249C41.9792 26.154 33.2711 26.154 27.9002 31.5249C22.5292 36.8959 22.5292 45.604 27.9002 50.9749L30.5502 53.6249L50.0002 73.0749L69.4502 53.6249L72.1002 50.9749C74.6802 48.3961 76.1297 44.8978 76.1297 41.2499C76.1297 37.6021 74.6802 34.1037 72.1002 31.5249Z" stroke="#232627" stroke-width="5" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
			</button> <br/><br/><br/>
			<button on:click={() => switchmode(1)} class="modeButton">
				<svg width="100" height="100" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
					<circle cx="50" cy="50" r="48" stroke="white" stroke-width="4"/>
					<path fill-rule="evenodd" clip-rule="evenodd" d="M39.8614 28.6027L36.6584 24.7632L25.1401 34.3722L28.3429 38.2117L39.8614 28.6027ZM63.3413 24.7638L74.8598 34.3728L71.6568 38.2123L60.1383 28.6033L63.3413 24.7638ZM51.2501 40.2373H47.5001V55.2373L59.3751 62.3623L61.2501 59.2873L51.2501 53.3623V40.2373ZM50.0001 30.2373C37.5751 30.2373 27.5001 40.3123 27.5001 52.7373C27.5001 65.1623 37.5751 75.2373 50.0001 75.2373C62.4251 75.2373 72.5001 65.1623 72.5001 52.7373C72.5001 40.3123 62.4251 30.2373 50.0001 30.2373ZM32.5001 52.7373C32.5001 62.3873 40.3501 70.2373 50.0001 70.2373C59.6501 70.2373 67.5001 62.3873 67.5001 52.7373C67.5001 43.0873 59.6501 35.2373 50.0001 35.2373C40.3501 35.2373 32.5001 43.0873 32.5001 52.7373Z" fill="white"/>
				</svg>
			</button>

		</div>
		<h1>deviants dice</h1>
		<div>
			<select bind:value={selected} on:change="{console.log(selected)}">
				{#each options as option}
					<option value={option.id}>
						{option.text}
					</option>
				{/each}
			</select>
		</div>
		<div class="parent">
			<div class="div1">
				<button class="optionButtons" on:click={() => reroll(1)}>
					{#if col1roll >= 0}
						{rawData['col1'][col1roll]}
					{:else}
						Roll the dice
					{/if}
				</button>
				<h3>{left[mode]}</h3>
			</div>
			<div class="div2">
				<button class="optionButtons" on:click={() => reroll(2)}>
					{#if col2roll >= 0}
						{rawData['col2'][col2roll]}
					{:else}
						Roll the dice
					{/if}
				</button>
				<h3>{right[mode]}</h3>
			</div>
		</div>
		<div class="rollDiv">
			<button class="rollButton" on:click={rollDie}>Roll</button>
		</div>
	</div>
</main>

<style>
:global(body) {
	background: #232627;
}
h1 {
	margin-top: 120px;
	margin-bottom: 80px;
	font-family: 'Lustria', serif;
	color: #fff;
	font-size: 72px;
	text-align: center;
}
h3 {
	font-family: Lato;
	font-style: normal;
	font-weight: 300;
	font-size: 48px;
	line-height: 58px;
	color: #FFFFFF;
}
select {
	width: 60%;
	margin-left: 20%
}
.container {
	padding-left: 100px;
	padding-right: 200px;
}
.parent {
	margin-top: 120px;
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	grid-template-rows: 1fr;
	grid-column-gap: 75px;
	grid-row-gap: 0px;
}

.div1 {
	grid-area: 1 / 1 / 2 / 2;
	text-align: center;
}
.div2 {
	grid-area: 1 / 2 / 2 / 3;
	text-align: center;
}
.optionButtons {
	padding-left: 150px;
	padding-right: 150px;
	padding-top: 45px;
	padding-bottom: 45px;
	margin-bottom: 20px;
	background: #3E4346;
	border-radius: 10px;
	font-family: Lato;
	font-style: normal;
	font-size: 48px;
	color: #FFFFFF;
}
.rollButton {
	margin-left: 37%;
	background: linear-gradient(108.12deg, #FF00B8 0%, #FF0038 100%);
	border-radius: 10px;
	width: 400px;
	font-family: Lato;
	font-style: normal;
	font-size: 72px;
	color: #FFFFFF;
}
.modeButtons {
	margin-top: 42vh;
	float: left;
}
.modeButton{
	all: unset;
	border: none;
	text-decoration: none;
	background: none;
	outline: none;
}
.modeButtons:active {
	border: none;
	text-decoration: none;
	background: none;
}
.help {
	all: unset;
	border: none;
	text-decoration: none;
	background: none;
	outline: none;
	float: right
}
</style>
