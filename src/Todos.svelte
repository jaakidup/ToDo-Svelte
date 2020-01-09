<script>
  import TodoItem from "./TodoItem.svelte";
  import { db } from "./firebase";
  import { collectionData } from "rxfire/firestore";
  import { startWith } from "rxjs/operators";

  export let uid;

  let text = "";

  const query = db
    .collection("todos")
    .where("uid", "==", uid)
    .orderBy("created");

  const todos = collectionData(query, "id").pipe(startWith([]));

  function add() {
    db.collection("todos").add({
      uid,
      text,
      complete: false,
      created: Date.now()
    });
    text = "";
  }

  function updateStatus(event) {
    console.log(event);
    const { id, newStatus } = event.detail;
    db.collection("todos")
      .doc(id)
      .update({ complete: newStatus });
  }

  function removeItem(event) {
    const { id } = event.detail;
    db.collection("todos")
      .doc(id)
      .delete();
  }
</script>

<style>
  input {
    display: block;
  }
</style>



<div class="">

  {#each $todos as todo}
    <TodoItem {...todo} on:remove={removeItem} on:toggle={updateStatus} />
  {/each}

</div>




<input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" bind:value={text} placeholder="Enter your todo"/>

<!-- <hr /> -->

<!-- <p>
  Your task:
  <strong>{text}</strong>
</p> -->

<button class="mt-2 bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow" on:click={add}>Add Task</button>
