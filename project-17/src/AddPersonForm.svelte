<!-- 
  
  Now, we'll create here a Custom Event Dispatcher.
  Although "Event Forwarding" can pass a function to our ancestor component, it can't do it with our data.
  That's why we'll create a custom event, passing our 'Persons' as objects to be handled in App.svelte.

-->

<script>
  import { createEventDispatcher } from 'svelte';       // We have to import the createEventDispatcher here.

  let dispatch = createEventDispatcher();               // Now we store the imported function in 'dispatch'.

  let name;
  let beltColour;
  let age;
  let skills = [];

  const handleSubmit = () => {        // Now we adjust our handleSubmit() function with the 'person' object.
    const person = {                   
      name,                           // This is the Javascript way of simplifying 'name: name'...
      beltColour,                     // ... 'beltColour: beltColour', 'age: age', skills: skills and so on.
      age, 
      skills,
      id: Math.random()               
      // id: Date.now().toString()    // This could be more accurate than using Math.random(). Test it later!
    }

    dispatch('addPerson', person);    // Finally, we dispatch our custom event name, plus our created 'person'.
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
  <input type="text" placeholder='name' bind:value={name}>
  <input type="number" placeholder='age' bind:value={age}>
  <label>Skills:</label>
  <!-- <input type="checkbox" bind:checked={fighting}>fighting<br>
  <input type="checkbox" bind:checked={sneaking}>sneaking<br>
  <input type="checkbox" bind:checked={running}>running<br> -->
  <input type="checkbox" bind:group={skills} value="fighting">fighting<br>
  <input type="checkbox" bind:group={skills} value="sneaking">sneaking<br>
  <input type="checkbox" bind:group={skills} value="running">running<br>
  <label>Belt colour:</label>
  <select bind:value={beltColour}>
    <option value="black">black</option>
    <option value="orange">orange</option>
    <option value="brown">brown</option>
    <option value="white">white</option>
  </select>
  <button>Add Ninja</button>
</form>