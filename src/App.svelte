<script>
	import { styles } from "./styles.js";
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

	<div class="meta">
		<div class="coordinates">Blocks: { Math.round(position / pixelPerBlock) }</div>
		<div>Score: 0</div>
	</div>

	<div class="me" use:styles={{jumpDuration: jumpDuration}}>
		<div class="shadow"></div>
		<div class="parrot">
			<img src="./parrot-leg-left.png" alt="Left Leg" class="parrot__leg parrot__leg--left">
			<img src="./parrot-leg-right.png" alt="Right Leg" class="parrot__leg parrot__leg--right">
			<img src="./parrot-without-legs.png" alt="Me" class="parrot__body">
		</div>
	</div>
</main>

<style lang="scss">

	main {
		padding: 1em;
		max-width: 100%;
		margin: 0 auto;
		height: calc(100% - 40px);
		background: url("../minecraft-bg.png");
		background-repeat: repeat-x;
		position: relative;
		background-position-y: -100px;
	}
	
	.me {
		position: absolute;
		top: 450px;
		left: 100px;
	}
	
	.me .parrot__body {
		position: absolute;
		height: auto;
		width: 100%;
		left: 10px;
		transition: transform 200ms ease;
	}
	
	.me .parrot {
		width: 80px;
		height: 140px;
		transform: translateY(0);
		transition-property: transform;
		transition-timing-function: ease;
		transition-duration: var(--jumpDuration);
	}

	.jump .me .parrot {
		transform: translateY(-100%);
	}

	@keyframes walk {
		0% {
			transform: rotate(60deg);
		}

		100% {
			transform: rotate(-30deg);
		}
	}

	.parrot__leg {
		position: absolute;
		height: auto;
		transform-origin: 50% 0;
		transition: all 200ms ease;
	}

	.parrot__leg--left {
		width: 15px;
		bottom: 25px;
		left: 47px;
	}

	.parrot__leg--right {
		width: 14px;
		bottom: 18px;
		left: 38px;
	}

	.running .parrot__body {
		transform: rotate(10deg);
	}

	.running .parrot__leg--left {
		bottom: 29px;
		left: 43px;
	}
	.running .parrot__leg--right {
		bottom: 22px;
		left: 35px;
	}

	.jump .parrot__body {
		transform: rotate(0deg);
	}

	.jump .parrot__leg {
		animation: unset;
	}

	.running .parrot__leg {
		animation: walk 200ms infinite alternate;
	}

	.running .parrot__leg--left {
		animation-delay: 200ms;
	}

	.shadow {
		position: absolute;
		width: 120%;
		height: 40px;
		background: rgba(0, 0, 0, 0.2);
		border-radius: 50%;
		bottom: 0;
	}

	.meta {
		color: #FFFFFF;
		text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
