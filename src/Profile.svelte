<script>
  export let displayName;
  export let photoURL;
  // export let uid;
</script>

<div class="flex mb-6 mt-6 items-center">
  <img class="rounded-full" src={photoURL} width="100" alt="user avatar" />
  <div class="text-3xl antialiased pl-5 text-justify">{displayName}</div>

  <!-- <p>Your userID is {uid}</p> -->
</div>
