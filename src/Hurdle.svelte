<script>
  export let height;
  export let position;
  export let spawnPosition;

  let h = height * 32;
</script>

<div
  class="hurdle"
  style={`
    height: ${h}px;
    transform: translateX(${spawnPosition - position}px);
    top: ${400 + (120 - h)}px
  `}>
</div>

<style>
  .hurdle {
    width: 50px;
    height: 50px;
    background: darkgray;
    position: absolute;
    right: -100px;
	}

	@media screen and (max-height: 600px) {
		.hurdle {
			top: 50%;
		}
  }
</style>
