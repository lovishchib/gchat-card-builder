<script>
	export let jsonText;

	import { currentEdit } from '$lib/stores/cardStore.js';
	import ButtonEditor from './ButtonEditor.svelte';
	import HeaderEditor from '$lib/Components/CardInputs/PropertyEditor/HeaderEditor.svelte';

	const handleHeaderUpdate = (field, value) => {
		jsonText = { ...jsonText, header: { ...jsonText.header, [field]: value } };
	};
	const handleButtonUpdate = (field, value, actionType, extraParams) => {
		let targetElement =
			jsonText.sections[$currentEdit.sIndex].widgets[$currentEdit.wIndex][$currentEdit.elementType][
				$currentEdit.elementIndex
			][$currentEdit.type];

		jsonText.sections[$currentEdit.sIndex].widgets[$currentEdit.wIndex][$currentEdit.elementType][
			$currentEdit.elementIndex
		][$currentEdit.type] = {
			...targetElement,
			onClick: value
		};
	};
</script>

<h5>Property Editor</h5>
<hr />
{#if $currentEdit}
	{#if $currentEdit.type === 'header'}
		<HeaderEditor headerData={jsonText.header} handleUpdate={handleHeaderUpdate} />
	{:else}
		Edit Section - {$currentEdit.sIndex} > Widget - {$currentEdit.wIndex} > {$currentEdit.elementType}-
		{$currentEdit.elementIndex} - {$currentEdit.type}
		{#if ['textButton', 'imageButton'].includes($currentEdit.type)}
			<ButtonEditor
				buttonData={jsonText.sections[$currentEdit.sIndex].widgets[$currentEdit.wIndex].buttons[
					$currentEdit.elementIndex
				][$currentEdit.type]}
				btnType={$currentEdit.type}
				handleUpdate={handleButtonUpdate}
			/>
		{/if}
		<!-- Edit {jsonText.sections[sIndex].widgets[wIndex].buttons[buttonIndex].textButton.text} -->
	{/if}
{/if}
