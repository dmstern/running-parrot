<script>
  export let startGame;
</script>

<div class="welcome-screen">
  <button class="btn-start" on:click={startGame}>Play</button>
</div>

<style>
  .welcome-screen {
    width: 400px;
    height: 300px;
    margin: 0 auto;
    padding-top: 200px;
  }

  .btn-start {
    width: 100px;
    line-height: 1.5em;
  }
</style>