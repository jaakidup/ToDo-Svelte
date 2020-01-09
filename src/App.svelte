<script>
  import Login from "./Login.svelte";
  import NavBar from "./Nav.svelte";
</script>

<style>
  main {
    max-width: 500px;
    margin-left: auto;
    margin-right: auto;
  }

</style>

<svelte:head>
  <!-- <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.7.4/css/bulma.min.css" /> -->

<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet">
</svelte:head>
<main class="content">

  <NavBar/>

  <Login/>

</main>
