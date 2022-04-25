### Svelte grammar study
- demo website: https://ddy-svelte-demo.surge.sh/
- study resource: [learning video on youtube](https://www.youtube.com/watch?v=zojEMeQGGHs&list=PL4cUxeGkcC9hlbrVO_2QFVqVPhlZmz7tO&index=1)


1、使用脚手架工具`degit` setting up a svelte app

```bash
'''
#-g means installing this package globally on my compute so we can use it anywhere in any directory
'''
npm install -g degit    #install degit with npm
degit sveltejs/template myproject   #create a project by degit
npm install #install dependency package with npm
npm run dev  #spin up a local development server to preview our project
```



2.语法

- Data bind

```javascript
//双向绑定
const handleInput = (e) => {
    name2 = e.target.value;
  };
<input type="text" on:input={handleInput}/>
  
//双向绑定(方式一)
const handleInput = (e) => {
    name2 = e.target.value;
  };
<input type="text" on:input={handleInput} value={name2} />
  
//双向绑定(方式二)
<input type="text" bind:value={name2} />

```

- React values

```javascript
//fullname实时变化
let firstname = "Duan";
let lastname = "Yu";
$: fullname = `${firstname} + ${lastname}`;
```

- loop

```javascript
{#each people as person}
    <div>
      <h4>{person.name}</h4>
      <p>{person.age} years old, {person.color} color</p>
    </div>
{:else}
    <p>there is no person</p>
{/each}
```

- inline event handlers

```javascript
<script>
  let people = [
    { name: "段誉1", color: "orange", age: 20, id: 1 },
    { name: "段誉2", color: "red", age: 21, id: 2 },
    { name: "段誉3", color: "black", age: 21, id: 3 },
  ];
  const handleClick = (e, id) => {
    people = people.filter((temp_person) => temp_person.id != id);
    console.log(e);
  };
</script>

<main>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      <p>{person.age} years old, {person.color} color</p>
      <button on:click={(e) => {handleClick(e, person.id);}}>delete</button>  
/*
注意这里：
	如果是<button on:click={handleClick(e, person.id)}}>delete</button>的话
	不点击button也会直接调用该函数，需要用一个函数来包裹该函数
	
原因:
	on:click={handleClick(e, person.id)}}是直接invoke funtion,没有declaration。
	
	Therefore, you need a function declaration, which will be invoked only by the click event and inside it you call your hander with as many arguments as you want.

SO解答：https://stackoverflow.com/questions/58262380/how-to-pass-parameters-to-onclick-in-svelte
*/  
    </div>
  {:else}
    <p>there is no person</p>
  {/each}
</main>
```

- conditions

```javascript
{#if num > 20}
  <p>num is bigger than 20</p>
{:else if num > 5}
  <p>num is bigger than 5</p>
{:else}
  <p>good choice</p>
{/if}
```

- css $ conditional styles

```javascript
<script>
  let showModal = true;
  let isPromo = true;
</script>

{#if showModal}
  <div class="backdrop" class:promo={isPromo}>   //conditional styles
    <div class="modal">
      <p>sign up for offers!</p>
    </div>
  </div>
{/if}

<style>
  .backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.8);
  }
  .modal {
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;
    text-align: center;
    background-color: white;
  }
  .promo .modal {
    background: crimson;
    color: white;
  }
</style>

```

- props

```javascript
//Modal.svelte
<script>
  export let message = "default message";
  let showModal = true;
  export let isPromo = false;
</script>

//App.svelte
<script>
  import Modal from "./Modal.svelte";
  let people = [
    { name: "段誉1", color: "orange", age: 20, id: 1 },
    { name: "段誉2", color: "red", age: 21, id: 2 },
    { name: "段誉3", color: "black", age: 21, id: 3 },
  ];
  const handleClick = (e, id) => {
    people = people.filter((temp_person) => temp_person.id != id);
    console.log(e);
  };
</script>

<Modal message="i am a good boy." isPromo={true} />

```

- Event forwarding

```javascript
//App.svelte
<Modal message="i am a good boy." {showModal} on:click={toggleModal} />

//Modal.svelte
{#if showModal}
  <div class="backdrop" class:promo={isPromo} on:click>
    <div class="modal">
      <p>{message}</p>
    </div>
  </div>
{/if}
 
 //注释：App是父，Modal是子继承了App，所以从App传进来的on:click可以直接在Modal中使用
```

- Event modifier

```javascript
//once - makes sure the event can only fire once (remove handler)
//preventDefault - prevent the default action (run e.preventDefault())
//self - only fires the event if the clicked element is the target
<p on:click|self>{message}</p>
<button on:click|once={toggleModal}>open the Modal</button>
```

- slot

```javascript
//App.svelte
<Modal {showModal} on:click={toggleModal}>
  <h3 slot="title">Add a new person</h3>
  <form>
    <input type="text" placeholder="name" />
    <input type="text" placeholder="color" />
    <button>Add Person</button>
  </form>
</Modal>

//Modal.svelte
#if showModal}
  <div class="backdrop" class:promo={isPromo} on:click|self>
    <div class="modal">
      <slot name="title" />
      <p>hello baby.</p>
      <slot />
    </div>
  </div>
{/if}
```

- Forms(part1)

```javascript
<form on:submit|preventDefault={handleSubimt}>   
  <input type="text" placeholder="name" bind:value={name} />
  <input type="text" placeholder="color" bind:value={color} />
  <input type="number" placeholder="age" bind:value={age} />
  <button>Add Person</button>
</form>
//在这preventDefault的作用是防止页面再次刷新(refresh)
//preventDefault - prevent the default action (run e.preventDefault())
//preventDefault - class event.preventDefault() before running the handler. Useful for client-side form handling, for example.
```

- Dispatching custom event

```javascript
//Modal.svelte
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

//App.svelte
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
```

