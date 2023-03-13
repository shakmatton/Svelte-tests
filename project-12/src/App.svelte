<script>
  import Modal from './Modal.svelte';

  let showModal = false;                          // We create a boolean value for the "showModal" variable...

  let toggleModal = () => {                       // ...and a toogleModal function
    showModal = !showModal;                       // when user clicks the backdrop, showmodal turns on/off
  };

	let people = [
    { name: 'yoshi', beltColour: 'black', age: 25, id: 1 },
    { name: 'mario', beltColour: 'orange', age: 45, id: 2 },
    { name: 'luigi', beltColour: 'brown', age: 35, id: 3 }
  ];

  const handleClick = (e, id) => {
    people = people.filter(person => person.id != id);
    console.log(e);
  };
</script>


<!-- Below, toogleModal is activated with the user click.
     The event "on:click" starts from the Modal.svelte component, and arrives here in App.svelte
     Now it is possible to "export an event" inside one component straight to an ancestor component (this one) -->

<Modal message='Hello, Ninjas!' {showModal} on:click={toggleModal} />  

<main>
  <button on:click|once={toggleModal}>Open Modal</button>
  <!-- the 'once' event modifier makes the toggleModal clickable only once, preventing new button click action -->

  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColour === 'black'}
        <p><strong>MASTER NINJA</strong></p>
      {/if}
      <p>{person.age} years old, {person.beltColour} belt.</p>
      <button on:click={(e) => handleClick(e, person.id)}>delete</button>
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