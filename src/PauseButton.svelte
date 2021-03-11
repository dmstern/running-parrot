<script>
  import PlayIcon from "./icons/Play.svelte";
  export let handleClick;
</script>

<button on:click={handleClick}>
  <PlayIcon/>
</button>

<style>

button {
  position: absolute;
  right: 10px;
  top: 10px;
  background: transparent;
  border: none;
  width: 3rem;
  height: 3rem;
  color: white;
}

</style>
