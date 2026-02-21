<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
  import { getDatabase, get, ref, update } from "firebase/database";
  import { firebase } from "../utils/firebase";

  const database = getDatabase(firebase);
  const rootReference = ref(database, "/");
  const vsReference = ref(database, "/versus");

  const versus = writable({
    home: {
      backgroundUrl: "",
      playerImages: ["", "", "", ""],
    },
    away: {
      backgroundUrl: "",
      playerImages: ["", "", "", ""],
    },
  });

  const players = writable([]);
  const teams = writable([]);

  const saveVersusScreen = () => {
    update(vsReference, $versus);
  };

  onMount(() => {
    get(rootReference).then((res) => {
      const data = res.val();
      if (data) {
        teams.set(data.teams.sort((x, y) => x.name.localeCompare(y.name)));
        players.set(data.players.sort((x, y) => x.name.localeCompare(y.name)));
      }
    });
  });
</script>

<h1>Manager</h1>

<div class="manager-container">
  <div class="home-team">
    <h2>Home Team</h2>
    <select name="home-team-select" bind:value={$versus.home.backgroundUrl}>
      <option value=""> ------ </option>
      {#each $teams as team}
        <option value={team.backgroundUrl}>{team.name}</option>
      {/each}
    </select>
    <h3>Players:</h3>
    <div>
      <select
        name="home-player-one-select"
        bind:value={$versus.home.playerImages[0]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
    <div>
      <select
        name="home-player-two-select"
        bind:value={$versus.home.playerImages[1]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
    <div>
      <select
        name="home-player-three-select"
        bind:value={$versus.home.playerImages[2]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
    <div>
      <select
        name="home-player-four-select"
        bind:value={$versus.home.playerImages[3]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
  </div>
  <div class="away-team">
    <h2>Away Team</h2>
    <select name="away-team-select" bind:value={$versus.away.backgroundUrl}>
      <option value=""> ------ </option>
      {#each $teams as team}
        <option value={team.backgroundUrl}>{team.name}</option>
      {/each}
    </select>
    <h3>Players:</h3>
    <div>
      <select
        name="away-player-one-select"
        bind:value={$versus.away.playerImages[0]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
    <div>
      <select
        name="away-player-two-select"
        bind:value={$versus.away.playerImages[1]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
    <div>
      <select
        name="away-player-three-select"
        bind:value={$versus.away.playerImages[2]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
    <div>
      <select
        name="away-player-four-select"
        bind:value={$versus.away.playerImages[3]}
      >
        <option value=""> ------ </option>
        {#each $players as player}
          <option value={player.pictureUrl}>{player.name}</option>
        {/each}
      </select>
    </div>
  </div>
</div>
<button on:click={saveVersusScreen}>Save</button>

<style>
  .manager-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 25px;
    margin-bottom: 20px;
  }
  select {
    width: 250px;
    margin-bottom: 10px;
  }
</style>
