<script>
  let color1 = "rea";
  let color2 = "black";
  const handleClick = () => {
    color2 = "orange";
  };
  const handleInput = (e) => {
    color2 = e.target.value;
  };
</script>

<main>
  <h1>Hello {color1}!</h1>
  <p style="color: {color2};">Hello ddy</p>
  <p>{color2} love {color2}</p>
  <button on:click={handleClick}>update info</button>
  <input type="text" on:input={handleInput} value={color2} />
  <!-- <input type="text" bind:value={color2} /> -->
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
