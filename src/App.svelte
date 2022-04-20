<script>
  let name = "ddy";
  let name2 = "caoqian";
  const handleClick = () => {
    name2 = "orange";
  };
</script>

<main>
  <h1>Hello {name}!</h1>
  <p>Hello ddy</p>
  <p>{name} love {name2}</p>
  <button on:click={handleClick}>update info</button>
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
