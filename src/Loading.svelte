<script>
  import { blur } from "svelte/transition";
  export let startGame;
  export let worldBG;
</script>

<div class="loading" in:blur>
  <div class="loading__animation">
    <div></div>
    <div></div>
    <div></div>
  </div>
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

	.loading__text {
    font-size: 1.5rem;
		margin-top: 0.5rem;
	}

  .loading__animation {
    display: flex;
    width: 100px;
    justify-content: space-between;
  }

  .loading__animation div {
    width: 20px;
    height: 20px;
    background-color: #5a4631;
    animation: load 900ms ease infinite;
  }

  .loading__animation div:nth-child(2) {
    animation-delay: 300ms;
  }

  .loading__animation div:nth-child(3) {
    animation-delay: 600ms;
  }

  @keyframes load {
    from {
      background-color: #1f1812;
    }
    
    to {
      background-color: #5a4631;
    }
  }
</style>
