<script>
	import { blur } from "svelte/transition";
	import Parrot from "./Parrot.svelte";
	import Meta from "./Meta.svelte";
	import Welcome from "./Welcome.svelte";
	import PauseButton from "./PauseButton.svelte";
	import LoadingAnimation from "./LoadingAnimation.svelte";

	let fps = 60;
	let playing = false;
	let running = false;
	let gameActive = false;
	let position = 0;
	let pixelPerFrame = 10;
	let interval = null;
	let jumpState = false;
	let jumpDuration = "400ms";
	let pixelPerBlock = 200;
	let isJumping = false;
	let loading = false;
	let worldBG = "../assets/minecraft-bg.png";
	let startGameAnimationDuration = 2000;

	let jumpKeys = ["ArrowUp", " "];
	let stopKeys = ["Escape", "ArrowLeft"];

	function loadGame() {
		loading = true;
	}
	
	function startGame() {
		loading = false;
		playing = true;

		setTimeout(() => {
			stage.focus();
			gameActive = true;
		}, startGameAnimationDuration);
	}

	function startRunning() {
		running = true
		interval = setInterval(() => {
			position += pixelPerFrame;
		}, 1000 / fps);
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

	function pause() {
		playing = false;
		gameActive = false;
		running = false;
		clearInterval(interval);
	}
	
	function handleKeydown(e) {
		if (jumpKeys.includes(e.key)) {
			triggerJump(e);
		} else if (stopKeys.includes(e.key)) {
			pause();
		}
	}

	function triggerJump(e) {
		e.preventDefault();

		if (!playing || !gameActive) {
			return;
		}

		if (!running) {
			startRunning();
		}

		if (!isJumping) {
			jump();
		}
	}

	function isTouchDevice() {
  	return (('ontouchstart' in window) ||
     (navigator.maxTouchPoints > 0) ||
     (navigator.msMaxTouchPoints > 0));
	}

</script>

<main
	class:jumpState
	class:running
	class:gameActive
	>
	<div
		id="stage"
		tabindex="0"
		class="stage"
		style={`background-image:url(${worldBG})`}
		on:keydown={handleKeydown}
		on:click={triggerJump}
	>
		<Meta position={position} pixelPerBlock={pixelPerBlock}/>
		<Parrot jumpDuration={jumpDuration} running={running} jump={jumpState} visible={gameActive}/>
	</div>
	{#if playing && !gameActive}
		<div class="help" transition:blur={{duration:500}}>
			<LoadingAnimation />
			{#if isTouchDevice()}
				Touch on the screen to jump and run
			{:else}
				Press [Space] or [🠕] to jump and run<br>
				Press [ESC] to pause
			{/if}
		</div>
	{/if}
		<PauseButton handleClick={pause}/>
	{#if !playing}
		<Welcome loadGame={loadGame} loading={loading} startGame={startGame} worldBG={worldBG} position={position} pixelPerBlock={pixelPerBlock}/>
	{/if}
</main>

<style lang="scss">

	.stage {
		height: 100%;
		background-repeat: repeat-x;
		padding: 1em;
		background-position-y: -100px;
		filter: blur(3px) brightness(0.7);
		transition: filter 2000ms ease;
	}

	@media screen and (max-height: 600px) {
		.stage {
			background-position-y: 50%;
		}
	}
	
	.gameActive .stage {
		filter: none;
	}

	main,
	.stage {
		animation-name: walk;
		animation-timing-function: linear;
		animation-duration: 6s;
		animation-iteration-count: infinite;
		animation-fill-mode: forwards;
		animation-play-state: paused;
	}
	
	main.running.gameActive,
	.running.gameActive .stage {
		animation-play-state: running;
	}

	@keyframes walk {
		from {
			background-position-x: 0;
		}

		to {
			background-position-x: -3840px;
		}
	}

	.help {
		width: 100%;
		color: white;
		position: absolute;
		top: 200px;
		font-size: 2rem;
		filter: none;
		text-align: center;
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
