<script>
	let roll = 0;
	let listLength = 10;
	function getRndInteger() {
	roll = Math.floor(Math.random() * (listLength - 0 + 1) ) + 0;
	}


</script>

<main>
	The roll is {roll}
	<button on:click={getRndInteger}>Roll the dice</button>
</main>

<style>

</style>