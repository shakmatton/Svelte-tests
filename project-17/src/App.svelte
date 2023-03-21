<script>
  import Modal from './Modal.svelte';
  import AddPersonForm from './AddPersonForm.svelte';      

  let showModal = false;

  let toggleModal = () => {
    showModal = !showModal;
  };

	let people = [
    // { name: 'yoshi', beltColour: 'black', age: 25, id: 1 },
    // { name: 'mario', beltColour: 'orange', age: 45, id: 2 },
    // { name: 'luigi', beltColour: 'brown', age: 35, id: 3 }
  ];

  const handleClick = (e, id) => {                
    people = people.filter(person => person.id != id);
    console.log(e);
  };

  // See full explanation of the function below in the following comments along the code.
  const addPerson = (e) => {       // The argument 'e' contains all implicit data which is passed through it. 
    //console.log(e.detail);       // All function data can be accessed within 'e.detail' (see the console).
    
    // REMEMBER: Svelte can only update a vector by explicitly reassigning it. So, let's do this trick below:
    const person = e.detail;       // A new variable now holds all the 'e.detail' content.
    people = [person, ...people];  // Update 'people' list by adding it first + the old 'people' list after.
    // The use of 'spread' operator (...) inserts the old contents of each old instance list into the new list.

    // Finally, we need to close the modal window after clicking 'ok'. For that, we can simply do this:
    showModal = false;
  };
</script>

<!-- Our AddPersonForm component lies inside our Modal component. -->
<!-- Notice how we add our custom 'addPerson' function, created inside AddPersonForm. -->
<!-- When a person is added, it will react to the addPerson function created above. -->      

<Modal {showModal} on:click={toggleModal}>       
  <AddPersonForm on:addPerson={addPerson} />     <!-- This will trigger inside the Modal component. -->
</Modal>

<main>
  <button on:click={toggleModal}>Open Modal</button>
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