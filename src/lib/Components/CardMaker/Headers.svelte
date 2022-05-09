<script>
	export let header;
	import { Grid, Row, Column, ImageLoader } from 'carbon-components-svelte';
	import { currentEdit } from '$lib/stores/cardStore.js';

	const handleHeaderClick = () => {
		currentEdit.set({ type: 'header' });
	};
</script>

{#if header}
	<div class="header-wrap" on:click={handleHeaderClick}>
		<span class="header-image">
			<ImageLoader src={header.imageUrl} />
		</span>
		<span class="header-content">
			<span>{header.title}</span>
			<div class="header-subtitle">{header.subtitle}</div></span
		>
	</div>
{/if}

<style>
	.header-wrap {
		display: flex;
		min-height: 56px;
		min-width: 200px;
		border: solid 1px rgba(0, 0, 0, 0.12);
		cursor: pointer;
	}

	.header-image {
		height: 32px;
		width: 32px;
		margin: 8px;
	}
	.header-content {
		padding: 8px;
	}
	.header-subtitle {
		color: rgba(117, 117, 117, 1);
		padding-top: 4px;
	}
</style>
