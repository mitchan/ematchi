<script lang="ts">
	import Game from './Game.svelte';

	import '../styles.css';
	import Modal from './Modal.svelte';
	import { levels } from './levelts';

	let state: 'idle' | 'playing' | 'lost' | 'won' = 'idle';
</script>

<Game />

{#if state !== 'playing'}
	<Modal>
		<header>
			<h1>e<span>match</span>i</h1>
			<p>the emoji matching game</p>
		</header>

		{#if state === 'won' || state === 'lost'}
			<p>you {state} the game</p>
		{:else if state === 'paused'}
			<p>game paused</p>
		{:else if state === 'idle'}
			<p>Choose a level</p>
		{/if}

		<div class="buttons">
			{#if state === 'paused'}
				<button>resume</button>
				<button>quit</button>
			{:else}
				{#each levels as level}
					<button>{level.label}</button>
				{/each}
			{/if}
		</div>
	</Modal>
{/if}

<style>
	h1 {
		font-size: 4em;
		font-family: Grandstander;
	}

	span {
		color: purple;
		font-family: Grandstander;
	}
</style>
