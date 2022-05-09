<script>
	export let buttonData;
	export let btnType;
	export let handleUpdate;
	import {
		FluidForm,
		TextInput,
		ContentSwitcher,
		Switch,
		Button,
		Toggle,
		Select,
		SelectItem,
		Grid,
		Row,
		Column
	} from 'carbon-components-svelte';
	import { ICON_TYPES } from '$lib/Constants/Constants.js';

	let selectedIndex = 0;
	let openurl = '';
	let actionMethodname = '';
	let iconUrlToggle = false;
	let parameterCounter = 0;
	let actionParams = [];

const removeParams = (index) => {
}
</script>

<br /><br />
<FluidForm>
	{#if btnType === 'textButton'}
		<TextInput
			labelText={'Text'}
			placeholder="Enter Text to Render..."
			bind:value={buttonData.text}
			required
			on:input={(event) => handleUpdate('text', event.target.value)}
		/>
	{:else}
		<Toggle bind:toggled={iconUrlToggle} labelText="Use Predefined Icons" />
		<br />
		{#if iconUrlToggle}
			<Select selected="">
				{#each ICON_TYPES as icon}
					<SelectItem value={icon} text={icon} />
				{/each}
			</Select>
			<br /><br />
		{:else}
			<TextInput
				labelText={'Icon Url'}
				placeholder="Enter Url for the ICON..."
				bind:value={buttonData.iconUrl}
				required
				on:input={(event) => handleUpdate('iconUrl', event.target.value)}
			/>
		{/if}
	{/if}
	<br />
	Click Action
	<br /><br />
	<ContentSwitcher bind:selectedIndex>
		<Switch text="Open Link" />
		<Switch text="Action" />
	</ContentSwitcher>
	{#if selectedIndex === 0}
		<TextInput
			labelText="Open URL"
			placeholder="Enter Url to Link..."
			value={openurl}
			on:input={(event) => handleUpdate('url', event.target.value, 'openLink')}
		/>
	{:else}
		<TextInput
			labelText="Action Method Name"
			placeholder="Enter Action Method Name..."
			bind:value={actionMethodname}
		/>
		<Grid>
			{#each Array(parameterCounter) as _, i}
				<Row>
					<Column>
						<TextInput
							labelText="Key 1"
							placeholder="key 1"
							bind:value={actionMethodname}
						/></Column
					>
					<Column>
						<TextInput
							labelText="Value 1"
							placeholder="Value 1"
							bind:value={actionMethodname}
						/></Column
					>
				</Row>
				<Button kind="ghost" onclick={() => removeParams(i)}>Remove this parameter</Button>
			{/each}
		</Grid>
		<Button kind="ghost" on:click={() => (parameterCounter = parameterCounter + 1)}
			>Add new Parameter</Button
		>
	{/if}
	<br />
	<Button>Save</Button>
</FluidForm>
