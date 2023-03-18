<!-- We create this new component so that we can avoid filling up our Modal.svelte component :) -->

<script>
  let name;
  let beltColour;
  let age;
  // let fighting = false;
  // let sneaking = false;
  // let running = false;
  let skills = [];                 // this will be used to store our checked values (see below in the code)

  const handleSubmit = () => {     // this just displays some info into our console
    console.log(name, beltColour, age, skills);
  };
</script>

<!-- When you submit a form, the default behaviour will refresh the page. 
     To combat this, we'll use an event modifier: "preventDefault". Check it out below:
  
     <form on:submit|preventDefault={handleSubmit}>                                              -->

<form on:submit|preventDefault={handleSubmit}>
  <input type="text" placeholder='name' bind:value={name}>
  <input type="number" placeholder='age' bind:value={age}>
  
  <label>Skills:</label>

  <!-- Following next: a new way of bind grouping check variables.
       We could do it like the lines commented below, but instead we'll use the bind:group modifier.
       It gets the checked value (true or false) and register it into the Skills[] array, creted above.
  -->

  <!-- <input type="checkbox" bind:checked={fighting}>fighting<br>
  <input type="checkbox" bind:checked={sneaking}>sneaking<br>
  <input type="checkbox" bind:checked={running}>running<br> -->
  <input type="checkbox" bind:group={skills} value="fighting">fighting<br>
  <input type="checkbox" bind:group={skills} value="sneaking">sneaking<br>
  <input type="checkbox" bind:group={skills} value="running">running<br>
  
  <label>Belt colour:</label>

  <!-- Now, for the select boxes, we'll just set the bind value to "beltColour", and that's it :) -->
  <select bind:value={beltColour}>
    <option value="black">black</option>
    <option value="orange">orange</option>
    <option value="brown">brown</option>
    <option value="white">white</option>
  </select>

  <button>Add Ninja</button>                                 <!-- Here we add our person (or ninja) -->

</form>