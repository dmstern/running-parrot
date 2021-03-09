<script>
	import { fly } from "svelte/transition";
	import Parrot from "./Parrot.svelte";
	import Meta from "./Meta.svelte";
	import Welcome from "./Welcome.svelte";

	let playing = false;
	let running = false;
	let position = 0;
	let pixelPerMilliSecond = 3;
	let interval = null;
	let jumpState = false;
	let jumpDuration = "400ms";
	let pixelPerBlock = 200;
	let isJumping = false;

	let jumpKeys = ["ArrowUp", " "];
	let walkKeys = ["ArrowRight", "w"];
	let stopKeys = ["Escape"];

	function startGame() {
		playing = true;
		main.focus();
	}

	function startRunning() {
		running = true
		interval = setInterval(() => {
			position += pixelPerMilliSecond;
		}, 1);
	}

	function dip() {
		jumpState = false;

		setTimeout(() => {
			isJumping = false;
		}, Number.parseInt(jumpDuration, 10) - 100);
	}

	function jump () {
		jumpState = true;
		isJumping = true;

		setTimeout(dip, Number.parseInt(jumpDuration, 10))
	}

	function stopRunning() {
		running = false;
		clearInterval(interval);
	}
	
	function handleKeydown(e) {
		if (walkKeys.includes(e.key) && !running) {
			startRunning();
		} else if (jumpKeys.includes(e.key) && !isJumping) {
			jump();
		} else if (stopKeys.includes(e.key)) {
			stopRunning();
		}
	}

</script>

<main
	id="main"
	tabindex="0"
	on:keydown={handleKeydown}
	style={`background-position-x: ${-position}px`}
	class:jumpState
	class:running
	>

	{#if playing}
		<div class="stage" style={`background-position-x: ${-position}px`} in:fly="{{ y: -200, duration: 2000 }}">
			<Meta position={position} pixelPerBlock={pixelPerBlock}/>
			<Parrot jumpDuration={jumpDuration} running={running} jump={jumpState}/>
		</div>
	{:else}
		<Welcome startGame={startGame}/>
	{/if}
</main>

<style lang="scss">

	.stage {
		background: url("../assets/minecraft-bg.png");
		height: 100%;
		background-repeat: repeat-x;
		padding: 1em;
		background-position-y: -100px;
	}
	
	main {
		max-width: 100%;
		margin: 0;
		height: 100%;
		background: url("../assets/minecraft-cleanstone.jpg");
		position: relative;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
