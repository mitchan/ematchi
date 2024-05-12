<script lang="ts">
	import { onMount } from 'svelte';
	import Countdown from './Countdown.svelte';
	import Found from './Found.svelte';
	import Grid from './Grid.svelte';
	import { levels } from './levelts';
	import type { Level } from './levelts';
	import { shuffle } from './utils';

	const level = levels[0];

	let size: number = level.size;
	let grid: string[] = create_grid(level);
	let found: string[] = [];
	let remaining = level.duration;
	let playing = true;

	function create_grid(level: Level): string[] {
		const copy = level.emojis.slice();
		const pairs: string[] = [];

		for (let i = 0; i < (level.size * level.size) / 2; i++) {
			const index = Math.floor(Math.random() * copy.length);
			const emoji = copy[index];

			// remove emoji
			copy.splice(index, 1);
			pairs.push(emoji);
		}

		pairs.push(...pairs);
		return shuffle(pairs);
	}

	function countdown() {
		let start = Date.now();
		let remaining_at_start = remaining;

		function loop() {
			if (!playing) {
				return;
			}

			requestAnimationFrame(loop);

			remaining = remaining_at_start - (Date.now() - start);

			if (remaining <= 0) {
				// TODO lost game
				playing = false;
			}
		}

		loop();
	}

	onMount(() => {
		countdown();
	});
</script>

<div class="game">
	<div class="info">
		<Countdown
			duration={level.duration}
			{remaining}
			on:click={() => {
				// TODO pause the game
			}}
		/>
	</div>

	<div class="grid-container">
		<Grid
			{grid}
			{found}
			on:found={(e) => {
				found = [...found, e.detail.emoji];

				if (found.length === (size * size) / 2) {
					// TODO won the game
				}
			}}
		/>
	</div>

	<div class="info">
		<Found {found} />
	</div>
</div>

<style>
	.game {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100%;
		font-size: min(1vmin, 0.5rem);
	}

	.info {
		width: 80em;
		height: 10em;
	}

	.grid-container {
		width: 80em;
		height: 80em;
	}
</style>
