<script>
  let firstname = "Duan";
  let lastname = "Yu";
  let color = "black";

  $: fullname = `${firstname} ${lastname}`;
  $: console.log(color);

  const handleClick = () => {
    color = "orange";
  };
  const handleInput = (e) => {
    color = e.target.value;
  };
</script>

<main>
  <p>{fullname} - {color}</p>
  <input type="text" bind:value={firstname} />
  <input type="text" bind:value={lastname} />
  <input type="text" bind:value={color} />
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
