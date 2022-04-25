<script>
  import AddPersonForm from "./AddPersonForm.svelte";
  import Modal from "./Modal.svelte";
  let showModal = false;
  let people = [
    { name: "段誉1", color: "orange", age: 20, id: 1 },
    { name: "段誉2", color: "red", age: 21, id: 2 },
    { name: "段誉3", color: "black", age: 21, id: 3 },
  ];
  const handleClick = (e, id) => {
    people = people.filter((temp_person) => temp_person.id != id);
    console.log(e);
  };
  const toggleModal = () => {
    showModal = !showModal;
  };
  const addPerson = (e) => {
    const person = e.detail;
    people = [person, ...people];
    showModal = false;
  };
</script>

<Modal {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson}>x</AddPersonForm>
</Modal>

<main>
  <button on:click={toggleModal}>open the Modal</button>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.color === "black"}
        <p><strong>good person color</strong></p>
      {/if}
      <p>{person.age} years old, {person.color} color</p>
      <button
        on:click={(e) => {
          handleClick(e, person.id);
        }}>delete</button
      >
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
