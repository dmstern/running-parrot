<script>;
  import { fly, blur } from "svelte/transition";
  import Loading from "./Loading.svelte";
  import Parrot from "./Parrot.svelte";
  import Meta from "./Meta.svelte";
  import PlayIcon from "./icons/Play.svelte";
  import RestartIcon from "./icons/Restart.svelte";
  export let loadGame;
  export let loading = false;
  export let startGame;
  export let worldBG;
  export let pixelPerBlock;
  export let position;
  export let gameStarted;
  export let restartGame;
</script>

<div class="welcome-screen" in:fly={{y: -500, duration: 1000, delay: 1000}} out:fly={{y: -500, duration: 1000}}>
  {#if loading}
    <Loading startGame={startGame} worldBG={worldBG}/>
  {:else}
    <div class="welcome-screen__main" out:blur={{duration:1000}}>
      <h1>Running Parrot</h1>
      {#if gameStarted}
      <div class="meta">
        <Meta position={position} pixelPerBlock={pixelPerBlock}/>
      </div>
      {/if}
      <Parrot staticPosition={true}/>
      <div class="buttons">
        {#if gameStarted}
        <button class="btn btn-restart" on:click={restartGame}><RestartIcon/><span> Restart</span></button>
        {/if}
        <button class="btn btn-play" on:click={loadGame}><PlayIcon/> <span>{#if gameStarted}Resume{:else}Start{/if}</span></button>
      </div>
    </div>
  {/if}
</div>

<style>
  h1 {
    color: white;
  }

  .welcome-screen {
    position: absolute;
    height: 100%;
    width: 100%;
    top: 0;
		align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: url("../assets/minecraft-cleanstone.jpg");
    opacity: 0.9;
  }

  .meta {
    padding: 20px;
  }

  .buttons {
    display: flex;
  }

  .btn {
    width: 150px;
    height: 60px;
    font-size: 1.5rem;
    border-width: 3px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .btn-restart {
    background-color: transparent;
    color: white;
    margin-right: 1em;
  }

  .welcome-screen__main {
    display: flex;
    flex-direction: column;
    justify-items: center;
    justify-content: space-between;
    align-items: center;
  }

</style>
