<script lang="ts">
	import { get_twemoji_url } from './utils';

	export let found: string[];
</script>

<div class="found">
	{#each found as emoji (emoji)}
		<img src={get_twemoji_url(emoji)} alt={emoji} />
	{/each}
</div>

<style>
	.found {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 0.5em;
	}

	img {
		height: 4em;
		width: 4em;
	}
</style>
