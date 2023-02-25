<script>
	// export let name;		// this keyword connects this variable with the props variable name	                        
	// let name;               // without that connection, the variable displays a null value...
	
	let firstName = 'Luke'
	let lastName = 'Skywalker'
	let beltColor = 'black'

	$: fullName = `${firstName} ${lastName}`     // string literals
	// $: console.log(beltColor)
	$: {                                         // the $ sign indicates a reactivity property 
		console.log(beltColor)                   // It will observe everything that changes inside $ block
		console.log(fullName)
	}

	
	const changeBeltColor = () => {
		beltColor = 'orange'
	}
	
	/*
	const changeNinjaName = () => {
	   	name = 'Mario'
	} 
	*/

	const handleInput = (e) => {        //  e = event / target = user text input / value = user text value
		beltColor = e.target.value      // each pressed key is displayed in the text box (our target)
	}
		
	

</script>

<main>

	<p>{fullName} - {beltColor} belt</p>
	<!-- <p>{firstName} {lastName} - {beltColor} belt</p> -->

	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
	<input type="text" bind:value={beltColor}>
	
		
	<!-- <p>{beltColor} belt</p> -->
	<!-- <p style="color: {beltColor}">{beltColor} belt</p>        Dynamic styling for belt colors -->

	<!-- <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->
	
	<!-- <button on:click={changeBeltColor}>Click here to update belt color</button>
	<button on:click={changeNinjaName}>Click here to update ninja name</button> -->
	
	<!-- <input type='text' on:input={handleInput}>    One-way binding: changes caused by user input -->
	<!-- <input type='text' value={beltColor}>         One-way binding: changes caused by variable value -->
	<!-- <input type='text' on:input={handleInput} value={beltColor}>      Two-way data binding -->
	<!-- <input type='text' bind:value={beltColor}>         Two-way data binding (the "Svelte way") -->
	

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	/* h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	} */

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>