<script>
	import anime from 'animejs';
	import { onMount } from 'svelte';
	import Draggable from './Draggable.svelte';

	let boxes = [];
	let i = 0;

	for(i=0; i < 20; i++){
		boxes.push({left:550 - i*10,top:(350 + i*10)})
	}

	var motionPath = function () {
		/*DEMO*/
		var path = anime.path('.motion-path-demo path');

		anime({
			targets: '.motion-path-demo .el',
			translateX: path('x'),
			translateY: path('y'),
			rotate: path('angle'),
			easing: 'linear',
			duration: 6000,
			loop: false
		});
		/*DEMO*/
		anime({
			targets: '.motion-path-demo .el',
			height: [{ value: 25 }, { value: 45 }, { value: 25 }],
			easing: 'easeOutQuad',
			duration: 6000,
			loop: false
		});
	};

	// onMount(async () => {
	// 	motionPath();
	// });
</script>

<button style="width:100px" on:click={motionPath}>run</button>

<div class="demo-content motion-path-demo">
	<div class="motion-path">
		<svg width="256" height="112" viewBox="0 0 256 112" class="path1">
			<path
				fill="none"
				stroke="currentColor"
				stroke-width="1"
				d="M8,56 C8,33.90861 25.90861,16 48,16 C70.09139,16 88,33.90861 88,56 C88,78.09139 105.90861,92 128,92 C150.09139,92 160,72 160,56 C160,40 148,24 128,24 C108,24 96,40 96,56 C96,72 105.90861,92 128,92 C154,93 168,78 168,56 C168,33.90861 185.90861,16 208,16 C230.09139,16 248,33.90861 248,56 C248,78.09139 230.09139,96 208,96 L48,96 C25.90861,96 8,78.09139 8,56 Z"
			/>
		</svg>

		<svg width="24" height="24" class="small square el follow-path">
			<rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
		</svg>

	</div>
</div>

{#each boxes as box}
	<Draggable bind:left = {box.left} bind:top = {box.top}>

		<h1>
			Drag Me
		</h1>
	</Draggable>
{/each}


<style>
	.square {
		position: absolute;
		top: 120px;
		left: 50px;
	}
	.path1 {
		position: absolute;
		top: 130px;
		left: 60px;
	}
</style>
