<script>
  import { createEventDispatcher } from "svelte";
  let dispatch = createEventDispatcher();
  let name;
  let color;
  let age;
  let skills = [];
  const handleSubimt = () => {
    const person = { name, color, age, skills, id: Math.random() };
    dispatch("addPerson", person);
  };
</script>

<form on:submit|preventDefault={handleSubimt}>
  <input type="text" placeholder="name" bind:value={name} />
  <input type="number" placeholder="age" bind:value={age} />
  <label>Skills:</label>
  <input type="checkbox" bind:group={skills} value="fighting" />fighting<br />
  <input type="checkbox" bind:group={skills} value="sneaking" />sneaking<br />
  <input type="checkbox" bind:group={skills} value="running" />fighting<br />
  <label>Color:</label>
  <select bind:value={color}>
    <option value="black">black</option>
    <option value="red">red</option>
    <option value="orange">orange</option>
  </select>
  <button>Add Person</button>
</form>

<style>
</style>
