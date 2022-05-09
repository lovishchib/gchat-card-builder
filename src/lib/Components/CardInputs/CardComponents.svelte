<script lang="ts">
	export let jsonText;
	import { Button } from 'carbon-components-svelte';

	const componentList = {
		header: { display: 'Header' },
		section: { display: 'Section' },
		btnSet: { display: 'Button Set' }
	};

	const handleComponentAdd = (event) => {
		switch (event.target.name) {
			case 'header': {
				if (!jsonText.hasOwnProperty('header')) {
					jsonText = {
						header: {
							title: 'Card header',
							subtitle: 'Subheader',
							imageUrl: 'https://source.unsplash.com/featured/320x180?nature&sig=8',
							imageStyle: 'IMAGE'
						},
						...jsonText
					};
				}
				break;
			}
			case 'section': {
				const newSxn = { widgets: [] };
				if (jsonText.hasOwnProperty('sections')) {
					const newSections = [...jsonText.sections];
					newSections.push(newSxn);
					jsonText = { ...jsonText, sections: newSections };
				} else jsonText = { ...jsonText, sections: [newSxn] };
				break;
			}
			case 'btnSet': {
				const newBtnSet = {
					buttons: [
						{
							imageButton: {
								iconUrl: 'https://storage.googleapis.com/images-io/pnt.png',
								onClick: {
									openLink: {
										url: 'https://pnt.redhat.com/pnt/p-15270185/RedHatConfirm...lesGuide1.pdf'
									}
								}
							}
						},
						{
							textButton: {
								text: 'confirmed stateside',
								onClick: {
									openLink: {
										url: 'https://pnt.redhat.com/pnt/p-15270185/RedHatConfirm...lesGuide1.pdf'
									}
								}
							}
						}
					]
				};
				const lastIndex = jsonText.sections.length - 1;
				const newWidget = [...jsonText.sections[lastIndex].widgets];
				newWidget.push(newBtnSet);
				jsonText = {
					...jsonText,
					sections: [...jsonText.sections.slice(0, lastIndex), { widgets: newWidget }]
				};
			}
		}
	};
</script>

<h5>Card Components</h5>
<hr />
<div class="card-comp-btns">
	{#each Object.keys(componentList) as component}
		<Button kind="secondary" name={component} on:click={handleComponentAdd}
			>{componentList[component].display}</Button
		><br /><br />
	{/each}
</div>

<style>
	:global(.card-comp-btns > .bx--btn--secondary) {
		width: 100%;
	}
</style>