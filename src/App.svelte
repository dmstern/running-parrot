<script>
	import { fly, blur } from "svelte/transition";
	import Parrot from "./Parrot.svelte";
	import Meta from "./Meta.svelte";
	import Welcome from "./Welcome.svelte";
	import Loading from "./Loading.svelte";
	// import PauseButton from "./PauseButton.svelte";

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
	// let stopKeys = ["Escape", "ArrowLeft"];

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

	// function stopRunning() {
	// 	running = false;
	// 	clearInterval(interval);
	// }
	
	function handleKeydown(e) {
		e.preventDefault();

		if (jumpKeys.includes(e.key)) {
			triggerJump(e);
		// } else if (stopKeys.includes(e.key)) {
			// stopRunning();
		}
	}

	function triggerJump(e) {
		e.preventDefault();

		if (!running) {
			startRunning();
		}

		if (!isJumping) {
			jump();
		}
	}

	function isMobile() {
		return window.innerWidth < 600;
	}

</script>

<main
	class:jumpState
	class:running
	class:gameActive
	>
	{#if loading}
		<Loading startGame={startGame} worldBG={worldBG}/>
	{:else if playing}
		<div
			id="stage"
			tabindex="0"
			class="stage"
			style={`background-image:url(${worldBG})`}
			in:fly="{{ y: -200, duration: startGameAnimationDuration }}"
			on:keydown={handleKeydown}
			on:click={triggerJump}
		>
			<Meta position={position} pixelPerBlock={pixelPerBlock}/>
			<Parrot jumpDuration={jumpDuration} running={running} jump={jumpState}/>
		</div>
		{#if !gameActive && !isMobile()}
			<div class="help" transition:blur>
				Press [Space] or [🠕] to jump and run<br>
				<!-- Press [ESC] to pause -->
			</div>
		{/if}
		<!-- <PauseButton handleClick={stopRunning}/> -->
	{:else}
		<Welcome loadGame={loadGame}/>
	{/if}
</main>

<style lang="scss">

	.stage {
		height: 100%;
		background-repeat: repeat-x;
		padding: 1em;
		background-position-y: -100px;
		filter: blur(3px) brightness(0.7);
		transition: blur 2000ms ease;
	}
	
	.gameActive .stage {
		filter: none;
	}

	main.running.gameActive,
	.running.gameActive .stage {
		animation-name: walk;
		animation-timing-function: linear;
		animation-duration: 6s;
		animation-iteration-count: infinite;
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
