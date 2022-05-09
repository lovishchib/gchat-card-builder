<script>
	export let jsonText;
    import { TextArea } from 'carbon-components-svelte';
    

	const handleJsonChange = (event) => {
		jsonText = JSON.parse(event.target.value);
	};
</script>

<h5>JSON Editor</h5>
<hr />
<TextArea
	rows={25}
	value={JSON.stringify(jsonText, null, 2)}
	on:change={handleJsonChange}
	placeholder="Enter a description..."
/>
