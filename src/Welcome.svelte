<script>
  import { blur } from "svelte/transition";
  export let loadGame;
</script>

<div class="welcome-screen" out:blur>
  <button class="btn-start" on:click={loadGame}>Play</button>
</div>

<style>
  .welcome-screen {
    position: absolute;
    height: 300px;
    width: 100%;
		padding-top: 200px;
    display: flex;
    justify-content: center;
  }

  .btn-start {
    width: 150px;
    font-size: 2rem;
  }
</style>
