<script>
	import { locations } from '../data/data';

	let currentLocation = locations[0];
	let current = 0;
	let points = 10;
	$: question = currentLocation.questions[current];

	function nextLocation() {
		const index = locations.indexOf(currentLocation);
		currentLocation = locations[index + 1];
		current = 0;
		points = 10;

		if (currentLocation === undefined) {
			alert('Nu är quizet slut!');
			currentLocation = locations[0];
			current = 0;
			points = 10;
		}
	}

	function nextQuestion() {
		current++;
		points -= 2;
	}

	function previousQuestion() {
		current--;
		points += 2;
	}

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>Vart är vi på väg?</h1>
	<h2><b>Resmål {locations.indexOf(currentLocation) + 1}</b></h2>
	<div>
		{#if points == 0}
			Svar: {currentLocation.location}
		{:else}
			<b>{points}</b>: {question}
		{/if}	
	</div>
	<div>
		{#if points == 0}
			<button on:click={nextLocation}>next</button>
		{:else}
			{#if current == 0}
				<button on:click={nextQuestion}>next</button>
			{:else}
				<button on:click={previousQuestion}>previous</button>
				<button on:click={nextQuestion}>next</button>
			{/if}
		{/if}	
	</div>
</section>

<style>

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
		gap: 1rem;
		font-size: 18px;
	}

	h1 {
		width: 100%;
	}
</style>
