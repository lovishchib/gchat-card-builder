<script>
	export let data;
	export let sIndex, wIndex;
	import { Button } from 'carbon-components-svelte';
	import TrashCan16 from 'carbon-icons-svelte/lib/TrashCan16';
	import { currentEdit } from '$lib/stores/cardStore.js';

	const handleClick = (btnType, index) => {
		currentEdit.set({
			sIndex: sIndex,
			wIndex: wIndex,
			elementType: 'buttons',
			elementIndex: index,
			type: btnType
		});
	};
</script>

<div class="button-row-wrap">
	<div class="shdw-button-row">
		{#each data.buttons as button, bIndex}
			{#if button.hasOwnProperty('imageButton')}
				<Button on:click={() => handleClick('imageButton', bIndex)} size="field" kind="ghost"
					><img
						class="shdw-button-image"
						src={button.imageButton.iconUrl}
						alt={'image-button'}
					/></Button
				>
			{:else}
				<Button on:click={() => handleClick('textButton', bIndex)} size="field" kind="ghost"
					><span class="shdw-button-text">{button.textButton.text}</span></Button
				>
			{/if}
		{/each}
	</div>
	<!-- <span style="padding: 4px"><Button kind="danger" icon={TrashCan16} /></span> -->
</div>

<style>
	.button-row-wrap {
		display: flex;
		justify-content: space-between;
		border: solid #ccc;
		border-width: 0.5px;
	}
	.shdw-button-image {
		height: 24px;
		width: 24px;
		margin: 10px;
	}
	.shdw-button-text {
		font-family: 'Roboto', sans-serif;
		font-size: 13px;
		font-weight: 500;
		text-transform: uppercase;
		line-height: 38px;
		padding: 0 8px;
		height: 40px;
		vertical-align: middle;
		border-radius: 3px;
	}

	.shdw-button-row {
		display: flex;
		flex-direction: row;
		align-items: center;
	}
</style>
