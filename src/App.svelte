<script>
	import Parrot from "./Parrot.svelte";
	import Meta from "./Meta.svelte";

	let running = false;
	let position = 0;
	let pixelPerMilliSecond = 3;
	let interval = null;
	let jump = false;
	let jumpDuration = "400ms";
	let pixelPerBlock = 200;
	let isJumping = false;

	let jumpKeys = ["ArrowUp", " "];
	let walkKeys = ["ArrowRight", "w"];

	function isWalkInput(e) {
		return walkKeys.includes(e.key);
	}

	function isJumpInput(e) {
		return jumpKeys.includes(e.key);
	}
	
	function handleKeydown(e) {
		if (isWalkInput(e)) {
			if (!running) {
				interval = setInterval(() => {
					position += pixelPerMilliSecond;
				}, 1)
			}

			running = true
		}

		if (isJumpInput(e) && !isJumping) {
			jump = true;
			isJumping = true;

			setTimeout(() => {
				jump = false;

				setTimeout(() => {
					isJumping = false;
				}, Number.parseInt(jumpDuration, 10) - 100);
			}, Number.parseInt(jumpDuration, 10))
		}
	}

	function handleKeyup(e) {
		if (isWalkInput(e)) {
			running = false;
			clearInterval(interval);
		}
	}
	
	function handleLoad() {
		let main = document.querySelector("#main");
		main.focus();
	}
</script>

<main
	id="main"
	tabindex="0"
	on:keydown={handleKeydown}
	on:keyup={handleKeyup}
	on:mouseenter={handleLoad}
	style={`background-position-x: ${-position}px`}
	class:jump
	class:running
	>
	<div class="stage" style={`background-position-x: ${-position}px`}>
		<Meta position={position} pixelPerBlock={pixelPerBlock}/>
		<Parrot jumpDuration={jumpDuration} running={running} jump={jump}/>
	</div>

</main>

<style lang="scss">

	.stage {
		background: url("../minecraft-bg.png");
		height: 100%;
		background-repeat: repeat-x;
		padding: 1em;
		background-position-y: -100px;
	}
	
	main {
		max-width: 100%;
		margin: 0;
		height: 100%;
		background: url("../minecraft-cleanstone.jpg");
		position: relative;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
