<script>
  import PauseIcon from "./icons/Pause.svelte";
  export let handleClick;
</script>

<button on:click={handleClick}>
  <PauseIcon/>
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
  font-size: 1.5rem;
}

</style>
