<script>
	import { styles } from "./styles.js";
	export let jumpDuration;
	export let jump = false;
	export let running = false;
</script>

<div class="me" class:jump class:running use:styles={{jumpDuration: jumpDuration}}>
  <div class="shadow"></div>
  <div class="parrot">
    <img src="./parrot-leg-left.png" alt="Left Leg" class="parrot__leg parrot__leg--left">
    <img src="./parrot-leg-right.png" alt="Right Leg" class="parrot__leg parrot__leg--right">
    <img src="./parrot-without-legs.png" alt="Me" class="parrot__body">
  </div>
</div>

<style lang="scss">
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

	.me.jump .parrot {
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

	.me.running .parrot__body {
		transform: rotate(10deg);
	}

	.me.running .parrot__leg--left {
		bottom: 29px;
		left: 43px;
	}
	.me.running .parrot__leg--right {
		bottom: 22px;
		left: 35px;
	}

	.me.jump .parrot__body {
		transform: rotate(0deg);
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
