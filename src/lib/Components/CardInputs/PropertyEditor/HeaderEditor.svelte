<script>
	export let headerData;
	import { FluidForm, TextInput, Select, FormGroup, SelectItem } from 'carbon-components-svelte';
	export let handleUpdate;
</script>

<FluidForm>
	{#if headerData}
		<TextInput
			labelText="Title"
			placeholder="Enter Title..."
			value={headerData.title}
			on:input={(event) => handleUpdate('title', event.target.value)}
		/>
		<TextInput
			labelText="Subtitle"
			placeholder="Enter Subtitle..."
			value={headerData.subtitle}
			on:input={(event) => handleUpdate('subtitle', event.target.value)}
		/>
		<TextInput
			labelText="Image URL"
			placeholder="Enter Image URL..."
			value={headerData.imageUrl}
			on:input={(event) => handleUpdate('imageUrl', event.target.value)}
		/>
		<br />
		IMAGE TYPE<Select
			selected={headerData.imageType}
			on:input={(event) => handleUpdate('imageStyle', event.target.value)}
		>
			<SelectItem value="IMAGE" text="IMAGE" />
			<SelectItem value="AVATAR" text="AVATAR" />
		</Select>
		<br />
	{/if}
</FluidForm>
