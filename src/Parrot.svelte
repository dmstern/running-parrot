<script>
	import { fly } from "svelte/transition";
	export let jumpDuration;
	export let jump = false;
	export let running = false;
	export let visible = true;
	export let staticPosition;
</script>

<div class="me" class:jump class:running class:staticPosition>
	{#if !staticPosition}
  	<div class="shadow"></div>
	{/if}
	{#if visible}
		<div class="parrot" transition:fly={{y:-200, duration: 800}} style={`transition-duration: ${jumpDuration}`}>
			<img src="./assets/parrot-leg-left.png" alt="Left Leg" class="parrot__leg parrot__leg--left">
			<img src="./assets/parrot-leg-right.png" alt="Right Leg" class="parrot__leg parrot__leg--right">
			<img src="./assets/parrot-without-legs.png" alt="Me" class="parrot__body">
		</div>
	{/if}
</div>

<style lang="scss">
  .me {
		position: absolute;
		top: 450px;
		left: 100px;
	}

	@media screen and (max-height: 600px) {
		.me {
			top: 50%;
		}
	}

	.me.staticPosition {
		position: static;
	}

	@media screen and (max-width: 600px) {
		.me {
			left: 30px;
		}
	}
	
	.me .parrot__body {
		position: absolute;
		height: auto;
		width: 100%;
		left: 10px;
		transition: transform 200ms ease;
	}

	@keyframes stand {
		10% {
			transform: rotate(-5deg)
		}

		20% {
			transform: rotate(5deg)
		}
		
		80% {
			transform: rotate(5deg)
		}

		90% {
			transform: rotate(-5deg);
		}

		100% {
			transform: rotate(0deg);
		}
	}

	.me.staticPosition .parrot__body {
		animation: stand 3s infinite ease;
	}

	.me.running .parrot__body {
		transform: rotate(10deg);
	}
	
	.me.jump .parrot__body {
		transform: rotate(0deg);
	}

	.me .parrot {
		width: 80px;
		height: 140px;
		transform: translateY(0);
		transition-property: transform;
		transition-timing-function: ease;
	}

	.me.jump .parrot {
		transform: translateY(-100%);
	}

	@keyframes walk {
		from {
			transform: rotate(60deg);
		}

		to {
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

	.me.running .parrot__leg--left {
		bottom: 29px;
		left: 43px;
	}
	.me.running .parrot__leg--right {
		bottom: 22px;
		left: 35px;
	}

	.me.jump .parrot__leg {
		animation: unset;
	}

	.me.running .parrot__leg {
		animation: walk 200ms infinite alternate;
	}

	.me.running .parrot__leg--left {
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
  
</style>
