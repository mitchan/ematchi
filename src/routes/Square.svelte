<script lang="ts">
	import { get_twemoji_url } from './utils';

	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
</script>

<div class="square" class:flipped={selected}>
	<button on:click />
	{#if !found}
		<img src={get_twemoji_url(emoji)} alt={emoji} />
	{/if}
</div>

<style>
	.square {
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: yellow;
	}

	.flipped button {
		background-color: red;
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	img {
		height: 6em;
		width: 6em;
		pointer-events: none;
	}
</style>
