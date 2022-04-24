<script>
  let name;
  let color;
  let age;
  const handleSubimt = () => {
    console.log(name, color, age);
  };
</script>

<form on:submit|preventDefault={handleSubimt}>
  <input type="text" placeholder="name" bind:value={name} />
  <input type="text" placeholder="color" bind:value={color} />
  <input type="number" placeholder="age" bind:value={age} />
  <button>Add Person</button>
</form>

<style>
</style>
