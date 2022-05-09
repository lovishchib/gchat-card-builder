<script>
	import { Grid, Row, Column } from 'carbon-components-svelte';
	import CardComponents from '$lib/Components/CardInputs/CardComponents.svelte';
	import PropertyEditor from '$lib/Components/CardInputs/PropertyEditor/PropertyEditor.svelte';
	import JsonEditor from '$lib/Components/CardInputs/JsonEditor.svelte';
	import CardWrapper from '$lib/Components/CardMaker/CardWrapper.svelte';

	import Card from '$lib/Components/Display/Card/Card.svelte';

	let jsonText = {
		sections: [
			{
				widgets: []
			}
		]
	};
	let renderCardObj;
	$: renderCardObj = { cards: [jsonText] };
	$: console.log(jsonText);
</script>

<Grid>
	<Row style="row">
		<Column lg={2}><div class="my-card"><CardComponents bind:jsonText /></div></Column>
		<Column lg={5}><div class="my-card"><CardWrapper cardData={renderCardObj} /></div></Column>
		<Column lg={4}><div class="my-card"><PropertyEditor bind:jsonText /></div></Column>
		<Column lg={5}><div class="my-card"><JsonEditor bind:jsonText /><div></Column>
	</Row>
</Grid>

<style>
	:global(.bx--grid) {
		max-width: inherit;
	}

	.my-card {
		background: white;
		min-height: 40rem;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
		transition: 0.3s;
		padding: 1rem;
	}
	.my-card:hover {
		box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
	}
</style>
