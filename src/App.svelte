<script>
  import { onMount } from "svelte";
  import { Route, Router } from "svelte-routing";
  import { getToken } from "./utils/tokenService";

  import Login from "./lib/Login.svelte";
  import VersusScreen from "./lib/VersusScreen.svelte";
  import Manager from "./lib/Manager.svelte";

  let isLoggedIn;
  let url = "";

  export const setLogin = () => {
    isLoggedIn = true;
  };

  onMount(() => {
    isLoggedIn = !!getToken();
  });
</script>

<Router {url}>
  <main>
    {#if isLoggedIn}
      <Route path="/" component={Manager} />
    {:else}
      <Route path="/"><Login {setLogin} /></Route>
    {/if}
    <Route path="/versus" component={VersusScreen} />
  </main>
</Router>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
