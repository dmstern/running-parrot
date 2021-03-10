<script>
  import { blur } from "svelte/transition";
  export let startGame;
</script>

<div class="loading" in:blur>
  <img class="loading__img" src="../assets/loading.svg" alt="Loading">
  <span class="loading__text">Loading...</span>
  <img src="../assets/minecraft-bg.png" alt="" on:load={startGame} style="display:none">
</div>

<style>
  .loading {
    position: absolute;
		display: flex;
    width: 100%;
		flex-direction: column;
		align-items: center;
    padding-top: 200px;
	}

	.loading__text {
    font-size: 1.5rem;
		margin-top: 0.5rem;
	}
</style>
