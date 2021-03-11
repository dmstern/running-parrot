<script>
  import { blur } from "svelte/transition";
  import LoadingAnimation from "./LoadingAnimation.svelte";
  export let startGame;
  export let worldBG;
</script>

<div class="loading" in:blur={{duration:1000}}>
  <LoadingAnimation />
  <span class="loading__text">Loading...</span>
  <img src={worldBG} alt="" on:load={startGame} style="display:none">
</div>

<style>
  .loading {
    position: absolute;
    top: 40%;
		display: flex;
    width: 100%;
		flex-direction: column;
		align-items: center;
    padding-top: 200px;
	}

  @media screen and (max-height: 600px) {
    .loading {
      top: 10px;
    }
  }

	.loading__text {
    font-size: 1.5rem;
		margin-top: 0.5rem;
	}

</style>
