<script>
	let people = [
		{ name: 'Ken', beltColor: 'red', age: 27, id: 1 },     // We use Svelte IDs here (read the comments)
		{ name: 'Ryu', beltColor: 'black', age: 28, id: 2 },
		{ name: 'Blanka', beltColor: 'green', age: 33, id: 3 }
	]
</script>

<main>
    <!-- Loop: array of 'people' searched by arbitrary variable 'person' using Svelte ID-->
	<!-- Svelte ID keeps track of which DOM element relates to which item in the array -->
	{#each people as person (person.id)}         
		<div>
			<h4>{person.name}</h4>
			<p>{person.age} years old, {person.beltColor} belt</p>
		</div>	
	{:else}                                      <!-- If the array of people is empty... -->
		<p>There are no people to show...</p>
	{/each}

</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>