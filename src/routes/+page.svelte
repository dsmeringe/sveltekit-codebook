<script>
/*
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
*/

import SvelteMarkdown from 'svelte-markdown';

let newContributionTitle = '';
let newContribution = "This could be your text..";
let entries = [
	{ title: 'example', content: 'cool stuff in md style' },
	{ title: 'second example', content: 'not cool stuff in md style' },
	{ title: 'third example', content: ' more\n\r # cool\n\r ```stuff``` in md style' }
]

function addItem () {
	entries = [...entries, {
		title: newContributionTitle,
		content: newContribution
	}];
	newContributionTitle = '';
	newContribution = '';
}

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		Inspirational code share
	</h1>

	<div class="inspiration-list">
		{#each entries as entry}
		<details>
			<summary>{entry.title}</summary>
			<SvelteMarkdown source={entry.content} />
		</details>
		{/each}
	</div>
</section>
<section>
	<label for="editor">Add new content using markup</label>
	<textarea 
		name="editor"
		class="editor" 
		contenteditable 
		bind:value={newContribution}
	/>
	<label>
		Title: 
		<input type="text" bind:value={newContributionTitle} />
	</label>
	<button on:click={addItem}>Add</button>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: left;
		flex: 0.6;
	}
	.inspiration-list {
		width: 100%;
	}
	summary {
		cursor: pointer;
	}
	details {
		padding:0.3em;
		transition: 1s;
		&:hover {
			background-color: #ccc;
			transition: 1s;
		}
		&[open] {
			background: #444;
			color: white;
			transition: 1px;
			
			& summary {
				font-weight: bold;
				background: #555;
				padding:0.3em;
				border-radius:3px;
				margin-bottom:0.3em;
				transition: 0.3s;
			}
		}
	}/*
	details > summary {
		list-style: none;
	}
	details > summary::marker, 
	details > summary::-webkit-details-marker {
		display: none;
	}*/

	.editor {
		border-top:1px solid silver;
		display: flex;
		flex-direction: column;
		justify-content: left;
		align-items: left;
		flex: 0.6;
		width:100%;
		padding: 0.5em;
		font-family: monospace;
	}

	h1 {
		width: 100%;
	}
</style>
