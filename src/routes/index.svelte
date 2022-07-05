<script context="module">
	export const prerender = true;
</script>

<script lang="ts">
	import { gsap } from 'gsap';
	import Flip from 'gsap/dist/Flip.js';
	import { onMount } from 'svelte';
	$: reorder = false;
	let state: any;

	gsap.registerPlugin(Flip);

	onMount(() => {
		state = Flip.getState('.group, .box');
	});
	const HandleClick = () => {
		reorder = !reorder;
		console.log(state, 'state');

		Flip.from(state, {
			absolute: true,
			duration: 0.5,
			stagger: 0.1,
			ease: 'power1.inOut'
		});
	};
</script>

<main>
	<h1>Smoothly change flex direction with GSAP's Flip plugin</h1>

	<button id="changeLayout" class="button" on:click={HandleClick}>change</button>
	<div class="container">
		<div class={reorder ? 'group' : 'group reorder'}>
			<div class="box">
				Common "FLIP" techniques employed by other tools won't work with flex elements because of
				the way browsers handle width/height.
			</div>
			<div class="box">
				Simply set <code>absolute: true</code> to have GSAP's Flip plugin make the elements position:
				absolute during the flip to work around challenges with flex and grid layouts.
			</div>
			<div class="box">
				When the flip animation is done, elements get reverted back to their normal positioning and
				everything appears seamless.
			</div>
			<div class="box">Happy flipping!</div>
		</div>
	</div>
</main>

<style lang="scss">
	main {
		background: #111;
		width: 100vw;
		height: 100vh;
	}

	h1 {
		color: white;
		font-weight: 400;
	}

	.group {
		width: 740px;
		height: auto;
		padding: 4px;
		background: #111;
		display: flex;
		flex-direction: column;
		overflow: hidden;
		color: black;
		position: relative;
		&.reorder {
			flex-direction: row;
		}
	}

	.box {
		margin: 4px;
		padding: 8px;
		font-size: 22px;
		line-height: 28px;
	}
	.box:nth-child(1) {
		background: rgba(85, 102, 205, 0.7);
	}
	.box:nth-child(2) {
		background: rgba(125, 70, 200, 0.7);
	}
	.box:nth-child(3) {
		background: rgba(33, 150, 243, 0.7);
	}
	.box:nth-child(4) {
		background: rgba(0, 188, 212, 0.7);
	}

	.button {
		padding: 10px 20px;
		margin-bottom: 10px;
	}

</style>
