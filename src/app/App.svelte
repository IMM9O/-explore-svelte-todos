<script>
  import { authState } from "rxfire/auth";
  import { auth, googleProvider } from "./firebase";

  import Layout from "./Layout.svelte";
  import Profile from "./Profile.svelte";
  import Todos from "./Todos.svelte";

  let user;

  const unsubscribe = authState(auth).subscribe(u => (user = u));

  function login() {
    auth.signInWithPopup(googleProvider);
  }
</script>

<Layout>

  <div slot="main-content">

    {#if user}
      <Profile {...user} />

      <button on:click={() => auth.signOut()}>Logout</button>

      <hr />
      <Todos uid={user.uid} />
    {:else}
      <button on:click={login}>Signin with Google</button>
    {/if}

  </div>
</Layout>
