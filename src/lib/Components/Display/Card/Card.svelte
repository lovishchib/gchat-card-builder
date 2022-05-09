<script lang="ts">
	export let jsonMessage;
	export let isReadOnly = true;
	let widgets = 'shdw-widgets';
	let keyValue = 'shdw-keyValue';
	let buttonRow = 'shdw-button-row';

	import { onMount } from 'svelte';
	import { Row, Column } from 'carbon-components-svelte';

	onMount(() => {
		jsonMessage && generateCard(jsonMessage);
	});
	const generateCard = (jsonMessage) => {
		if (!jsonMessage) return;
		try {
			let cardElement = document.getElementById('shdw-sections');
			let visualCard = document.getElementById('shdw-visual-card');
			cardElement && visualCard && visualCard.removeChild(cardElement);
			crawlJson(jsonMessage);
		} catch (error) {
			console.error('Error in generating card');
			console.log(error);
		}
		// toggled = !toggled;
		// toggleCardVisibility();
	};
	$: !isReadOnly && generateCard(jsonMessage);
	const crawlJson = (obj) => {
		if (obj === undefined) return [];

		Object.keys(obj).forEach((k) => {
			if (obj[k] && typeof obj[k] === 'object') {
				appendHtmlElement(k, obj[k]);
				return crawlJson(obj[k]);
			}
			appendHtmlElement(k, obj[k]);
		});
	};

	const appendHtmlElement = (k, obj) => {
		// console.log("key: " + k);
		// console.log("object: " + obj);
		switch (k) {
			case 'cards':
				return;
			case 'header': {
				injectHtml('shdw-visual-card', `<div class="shdw-header" id="shdw-card-header" />`);
				break;
			}
			case 'title': {
				injectHtml(
					'shdw-card-header',
					`<div class="header-text" id="shdw-header-text"><div class="shdw-header-title">${obj}</div></div>`
				);
				break;
			}
			case 'subtitle': {
				appendHtml('shdw-header-text', 'shdw-header-subtitle', obj);
				break;
			}
			case 'imageUrl': {
				injectFirstChild('shdw-card-header', obj);
				break;
			}
			case 'sections': {
				appendHtml('shdw-visual-card', 'shdw-sections', '', 'shdw-sections');
				break;
			}
			case 'widgets': {
				widgets += '1';
				appendHtml('shdw-sections', 'shdw-widgets', '', widgets);
				break;
			}
			case 'keyValue': {
				keyValue += '1';
				appendHtml(widgets, 'shdw-keyValue', '', keyValue);
				break;
			}
			case 'topLabel': {
				appendHtml(keyValue, 'shdw-keyValue-key', obj, '');
				break;
			}
			case 'content': {
				appendHtml(keyValue, 'shdw-keyValue-value', obj, '');
				break;
			}
			case 'buttons': {
				buttonRow += '1';
				appendHtml(widgets, 'shdw-button-row', '', buttonRow);
				break;
			}
			case 'imageButton': {
				let imageBtn = buildImageButton(obj);
				document.getElementById(buttonRow).appendChild(imageBtn);
				break;
			}
			case 'textButton': {
				let textBtn = buildTextButton(obj);
				document.getElementById(buttonRow).appendChild(textBtn);
				break;
			}
		}
	};

	const appendHtml = (parentId, cls, val = '', id = '') => {
		var div = document.createElement('div');
		div.classList.add(cls);
		if (val !== '') div.innerText = val;
		if (id !== '') div.id = id;
		document.getElementById(parentId)?.appendChild(div);
	};

	const injectHtml = (id, html) => {
		const element = document.getElementById(id);
		if (element) element.innerHTML = html;
	};

	const buildImageButton = (obj) => {
		let imageBtn = document.createElement('img');
		imageBtn.classList.add('shdw-button-image');
		if (obj.iconUrl) imageBtn.src = obj.iconUrl;
		if (obj.icon)
			imageBtn.src =
				'https://www.materialui.co/materialIcons/av/play_circle_filled_black_24x24.png';
		// TODO: implement google icon lookup
		imageBtn.onclick = () => {
			// window.open(obj.onClick.openLink.url, "_blank");
		};
		return imageBtn;
	};

	const buildTextButton = (obj) => {
		let textBtn = document.createElement('div');
		textBtn.classList.add('shdw-button-text');
		textBtn.innerText = obj && obj.text;
		textBtn.onclick = () => {
			// window.open(obj.onClick.openLink.url, "_blank");
		};
		return textBtn;
	};

	const injectFirstChild = (id, val) => {
		let img = document.createElement('img');
		img.classList.add('sdhw-header-icon');
		img.alt = 'main card image';
		img.src = val;
		let header = document.getElementById(id);
		header.insertBefore(img, header.firstChild);
	};
</script>

<div class="shdw-card-container" id="shdw-card-container">
	<div id="shdw-visual-card" class="shdw-visual-card" />
</div>

<style>
	.shdw-card-container {
		background-color: rgba(0, 0, 0, 0.22);
		z-index: -1;
		overflow: auto;
		display: flex;
		width: 100%;
		padding: 1rem;
		justify-content: center;
	}

	.shdw-visual-card {
		border: 1px solid rgba(0, 0, 0, 0.12);
		background: white;
		width: 320px;
	}

	:global(.shdw-header) {
		display: flex;
		flex-direction: row;
		align-items: center;
		padding-left: 8px;
	}

	:global(.sdhw-header-icon) {
		height: 32px;
		width: 32px;
		margin-right: 8px;
		object-fit: cover;
	}

	:global(.shdw-header-text) {
		display: flex;
		flex-direction: column;
	}

	:global(.shdw-header-title) {
		flex-grow: 1;
		font-family: 'Roboto', sans-serif;
		font-size: 13px;
		color: rgb(33, 33, 33);
		line-height: 20px;
	}

	:global(.shdw-header-subtitle) {
		flex-grow: 1;
		line-height: 20px;
		font-family: 'Roboto', sans-serif;
		font-size: 13px;
		color: rgb(117, 117, 117);
	}

	:global(.shdw-sections) {
		display: flex;
		flex-direction: column;
	}

	:global(.shdw-widgets) {
		border-top: 1px solid rgba(0, 0, 0, 0.12);
		display: flex;
		flex-direction: column;
		padding: 8px 0px;
	}

	:global(.shdw-keyValue) {
		display: flex;
		flex-direction: column;
		padding: 4px 8px;
	}

	:global(.shdw-keyValue-key) {
		color: rgb(117, 117, 117);
		font-family: 'Roboto', sans-serif;
		font-size: 12px;
		line-height: 16px;
	}

	:global(.shdw-keyValue-value) {
		color: rgb(33, 33, 33);
		font-family: 'Roboto', sans-serif;
		font-size: 13px;
		line-height: 22px;
	}

/* 	:global(.shdw-button-row) {
		display: flex;
		flex-direction: row;
		align-items: center;
	} */

/* 	:global(.shdw-button-text) {
		font-family: 'Roboto', sans-serif;
		font-size: 13px;
		font-weight: 500;
		color: rgb(30, 136, 229);
		text-transform: uppercase;
		line-height: 38px;
		padding: 0 8px;
		height: 40px;
		vertical-align: middle;
		border-radius: 3px;
	}

	:global(.shdw-button-text:hover) {
		background-color: rgba(30, 136, 229, 0.12);
		cursor: pointer;
	}

	:global(.shdw-button-image) {
		height: 24px;
		width: 24px;
		margin: 10px;
	} */
</style>
