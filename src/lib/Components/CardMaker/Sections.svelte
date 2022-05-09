<script>
	export let sections;

	import TextParagraph from './Widgets/TextParagraph.svelte';
	import ImageWidget from './Widgets/ImageWidget.svelte';
	import ButtonWidget from './Widgets/ButtonWidget.svelte';
	import KeyValue from './Widgets/KeyValue.svelte';
</script>

{#each sections as section, sIndex}
	{#each section.widgets as widget, wIndex}
		{#if widget.hasOwnProperty('textParagraph')}
			<TextParagraph data={widget} />
		{:else if widget.hasOwnProperty('image')}
			<ImageWidget data={widget} />
		{:else if widget.hasOwnProperty('keyValue')}
			<KeyValue data={widget} />
		{:else if widget.hasOwnProperty('buttons')}
			<ButtonWidget data={widget} {sIndex} {wIndex} />
		{:else}
			<span> click to add widget components </span>
		{/if}
	{/each}
{/each}
