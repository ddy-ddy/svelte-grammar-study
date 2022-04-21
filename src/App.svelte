<script>
  let people = [
    { name: "段誉1", color: "orange", age: 20, id: 1 },
    { name: "段誉2", color: "red", age: 21, id: 1 },
    { name: "段誉3", color: "black", age: 21, id: 1 },
  ];
</script>

<main>
  {#each people as person}
    <div>
      <h4>{person.name}</h4>
      <p>{person.age} years old, {person.color} color</p>
    </div>
  {:else}
    <p>there is no person</p>
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
