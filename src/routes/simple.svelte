<script>
	import { gsap } from 'gsap';
	import Flip from 'gsap/dist/Flip.js';
	import { onMount } from 'svelte';

	gsap.registerPlugin(Flip);

	onMount(() => {
		const squares = gsap.utils.toArray('.square');

		function doFlip() {
			// Get the initial state
			const state = Flip.getState(squares);

			// Make DOM or styling changes (swap the squares in our case)
			swap(squares);

			// Animate from the initial state to the end state
			Flip.from(state, { duration: 2, ease: 'power1.inOut' });
		}

		function swap([a, b]) {
			a.parentNode.children[0] === a ? a.parentNode.appendChild(a) : a.parentNode.appendChild(b);
		}

		document.addEventListener('click', doFlip);
	});
</script>

<div class="container">
	<div class="square" id="sq1">1</div>
	<div class="square" id="sq2">2</div>
</div>

<style>
	.container {
		display: -webkit-box;
		display: flex;
		-webkit-box-pack: justify;
		justify-content: space-between;
	}

	.square {
		width: 100px;
		height: 100px;
		font-size: 3em;
		display: -webkit-box;
		display: flex;
		-webkit-box-pack: center;
		justify-content: center;
		-webkit-box-align: center;
		align-items: center;
		color: black;
		background-color: #88ce02;
		cursor: pointer;
	}
</style>
