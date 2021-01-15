<div>
	<ul>
		{#each [ ...tags.values() ] as tag (tag)}
		<li animate:flip={{ duration: 200 }} style="background-color: {colour(tag)};">
			<span>{tag}</span>
			<button on:click={() => removeTag(tag)}>⨯</button></li>
		{/each}
		<li class="input">
			<input type="text" on:keyup={handleInput} on:blur={parseInput} bind:value={current} />
		</li>
	</ul>
</div>

<style>
	div {
		display: flex;
		border: 1px solid grey;
		flex-wrap: wrap;
	}
	
	input {
		border: 0;
		outline: 0;
		display: flex;
		margin: 0;
		padding: 3px 0;
		width: 100%;
	}
	
	ul {
		list-style-type: none;
		display: flex;
		padding: 0;
		margin: 0;
		flex-wrap: wrap;
	}
	
	li {
		border-radius: 5px;
		padding: 6px;
		margin: 3px;
		flex-direction: row;
    display: flex;
		align-items: center;
		white-space: nowrap;
	}

	li.input {
		background: transparent;
		margin: 0;
		padding: 0;
		width: 100%;
    flex: 1;
	}
	
	li span {
		line-height: inherit;
	}
	
	button {
		border: 0;
		outline: 0;
		background-color: transparent;
		padding: 0;
		margin: 0;
		font-weight: bold;
		margin: 0 3px;
    color: inherit;
	}

  button:hover {
    transition: color 0.2s ease-in-out;
    color: white;
  }
</style>

<script>
	import { flip } from 'svelte/animate'
	
	export let delimiter = ','
	export let tags = new Set([])
	export let colour = (tag) => {
		if ( tag.length <= 0 ) { return 0 }
		let h = 0
		let i = 0
		while (i < tag.length) {
			h = (h << 5) - h + tag.charCodeAt(i++) | 0
		}
		return 'hsl(' + (h / 360) + ', 100%, 80%)'
	}
	
	let current = ''
	
	function parseInput () {
		current.split(delimiter).forEach(addTag)
		current = ''
		tags = tags
	}
	
	function addTag (tag) {
		const clean = tag && tag.trim()
		clean && clean !== '' && tags.add(tag)
	}
	
	function handleInput ({ key, code }) {
		(key === delimiter || code === 'Enter') && parseInput()
	}
	
	function removeTag (tag) {
		tags.delete(tag)
		tags = tags
	}
</script>