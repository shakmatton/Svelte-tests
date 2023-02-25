<script>
	let people = [
		{name: 'Ken', age: 28, beltColor: 'red', id: 1},
		{name: 'Ryu', age: 29, beltColor: 'black', id: 2},
		{name: 'Blanka', age: 35, beltColor: 'green', id: 3}
	]

	const handleClick = (id) => {
		// We'll remove the curly braces inside the function. Check the comments to know why.
		people = people.filter(person => person.id != id)   
		/* 
		   This will update our people array, filtering the ids of the people we want remove from it.
		   We must reassign the people array (by using '='), so we can have a new updated array.	

		   The logic is this: filter() keeps our person if the 'person.id != id' returns true.
		   Otherwise, if it returns false, the function will remove the person from the array.    
		*/ 
	}

</script>

<main>

	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			<p>{person.age} years old, {person.beltColor} belt.</p>

			<!-- The following line has a problem:
				 if you pass a function directly, like below, it will be triggered automatically.
				 
				 This is a Javascript thing: 
				 if the function ends in 'function()', it might be called straight away.
				 
				 Instead of using '{handleClick(person.id)}', we'll create an indirect function.
				 From inside there, 'handleClick' function will be called only when the user triggers it.
			
				 Let's comment the following line: <button on:click={handleClick(person.id)}>Delete</button>
				 We'll replace it for an inline function, which won't be invoked:
				'<button on:click={ () => {} }>Delete</button>'	 
				This is an anonymous function. Notice we don't have parenthesis after the arrow.
				It's just a reference to a function which runs when we the user click it.

				For example: 
				'<button on:click={() => {console.log('click me')}}>Delete</button>'	 
				 This is going to run only when we click on a button (and not automatically, as before).				 
				 

			<button on:click={() => {handleClick(person.id)}}>Delete</button>
			<!-- Ok, this is fine. But since it's an inline function, we can get rid of the curly braces:  -->

			<button on:click={() => handleClick(person.id)}>Delete</button>

			<!-- Now, the way we did above is fine: our 'handleClick' function ends with parenthesis.
				 But the left function '()' wraps the function to the right 'handleClick(...)'.
				 One function sits inside another, and it's not invoked unless we click on the button.

				 See how we implement the logic inside the script session.
			-->

			<!-- You could also pass 'e' as a parameter for getting all the function events in the console:
				<button on:click={(e) => handleClick(e, person.id)}>Delete</button>

			And, in the script session:
				const handleClick = (e, id) => { ... 
			-->


<!-- If you want avoid bloating the markup with the anonymous function, just separate logic from markup:
	
	<main> 
		[...]
		<button on:click={handleClick(person.id)}>delete</button>
	</main> 

	<script>
	
	[...]
	const handleClick = (id) => {      
		return () => { people = people.filter(person => person.id != id); }
		// This closure will be returned as the callback we need
	}
	</script>
		
-->

	{#if person.beltColor === 'black'}
		<p>MASTER OF THEM ALL!</p>
	{:else if person.beltColor ==='red'}
		<p>ALMOST THERE!</p>
	{:else}
		<p>THERE'S A LONG WAY AHEAD...</p>
	{/if}


		</div>

	{:else}
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