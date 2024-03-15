<script>
  // @ts-nocheck

  let toDoList = [];
  let textInput = "";

  function addTodo() {
    if (textInput.trim() === "") {
      alert("enter todo");
      return;
    }
    toDoList = [
      ...toDoList,
      {
        content: textInput,
        editing: false,
        checked: false,
      },
    ];
    textInput=""
  }

  function setEditing(i, isEditing) {
    toDoList[i].editing = isEditing;
  }

  function deleteTodo(i) {
    // console.log("####", i);
    toDoList.splice(i, 1);
    toDoList = toDoList;
  }
</script>

<svelte:head>
  <title>Home</title>
  <meta name="description" content="To do demo app" />
</svelte:head>

<section>
  <div style="margin: 0 auto; padding: 20px; width: 700px;">
    <h1>To Do List</h1>
    <p>Enter your Todo here</p>
    <div style="display: flex">
      <input type="text" bind:value={textInput} />
      <button style="width: 200px" on:click={addTodo}> Add </button>
    </div>
  </div>
</section>

{#each toDoList as toDo, i}
  <div>
    {#if toDo.editing}
      <input type="text" bind:value={toDo.content} />
    {:else}
      <input type="checkbox" bind:checked={toDo.checked} />
      <h4 style={`${toDo.checked ? "text-decoration: line-through" : ""}`}>
        {toDo.content}
      </h4>
    {/if}
    <div style="display: flex">
      {#if toDo.editing}
        <!-- svelte-ignore missing-declaration -->
        <button on:click={() => setEditing(i, false)}> Save </button>
      {:else}
        <!-- svelte-ignore missing-declaration -->
        <button on:click={() => setEditing(i, true)}> Edit </button>
      {/if}
      <!-- svelte-ignore missing-declaration -->
      <button on:click={() => deleteTodo(i)}> Delete </button>
    </div>
  </div>
{/each}

<style>
</style>
