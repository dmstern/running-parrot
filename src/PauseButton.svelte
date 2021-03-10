<script>
  export let handleClick;
</script>

<button on:click={handleClick}>
  <svg class="icon-pause" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 9v6m4-6v6m7-3a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
</button>

<style>

button {
    position: absolute;
    right: 0;
    top: 0;
    background: transparent;
    border: none;
    width: 3rem;
    height: 3rem;
  }

  .icon-pause {
    color: white;
  }

</style>
