<script>
	export let cardData;
	import Headers from './Headers.svelte';
	import Sections from './Sections.svelte';
</script>

<h5>Rendered Card</h5>
<hr />
<div class="card-wrapper">
	<Headers header={cardData.cards[0].header} />
	<Sections sections={cardData.cards[0].sections} />
</div>

<style>
	.card-wrapper {
		width: 320px;
		font-family: 'Roboto', sans-serif;
		font-size: 1em;
		background: #fff;
		border: solid 1px #ccc;
	}
</style>
