<script>;
  import { fly, blur } from "svelte/transition";
  import Loading from "./Loading.svelte";
  import Parrot from "./Parrot.svelte";
  export let loadGame;
  export let loading = false;
  export let startGame;
  export let worldBG;
</script>

<div class="welcome-screen" transition:fly={{y: -500, duration: 1000}}>
  {#if loading}
  <Loading startGame={startGame} worldBG={worldBG}/>
  {:else}
    <h1 out:blur>Running Parrot</h1>
    <Parrot staticPosition={true}/>
    <button out:blur class="btn-start" on:click={loadGame}>Play</button>
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

  .btn-start {
    width: 150px;
    height: 60px;
    font-size: 1.5rem;
  }
</style>
