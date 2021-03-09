<script>
  export let position;
  export let pixelPerBlock;
</script>

<div class="meta">
  <div class="coordinates">Blocks: { Math.round(position / pixelPerBlock) }</div>
  <div>Score: 0</div>
</div>

<style>
  .meta {
		color: #FFFFFF;
		text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
	}

</style>
