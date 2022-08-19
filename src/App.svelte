<script>
import Loader from "./Loader.svelte";
import WordData from "./WordData.svelte";

let word = "";
let loading = false;
let wordData = null;

const searchWord = async () => {
	if(word.length === 0) return;

	loading = true;
	wordData = null;
	try {
		let res = await fetch("https://api.dictionaryapi.dev/api/v2/entries/en/"+word);
		const data = await res.json()
		if(Array.isArray(data)) wordData = data[0]
		else wordData = "No result"

		loading = false;
	} catch (error) {
		loading = false;
	}
}
</script>

<main>
	<div class="header">Dictionary App</div>

	<div class="center">
		<div class="form">
			<div class="form-group">
				<span>Search Word</span>
				<input type="text" placeholder="Type word here" bind:value={word} />
			</div>
			<div class="form-group">
				<button on:click={searchWord}>Search</button>
			</div>
		</div>

		{#if loading === true || wordData !== null}
		<div class="result">
			{#if wordData !== null && typeof wordData !== 'string'}
			<WordData wordData={wordData} />
			{:else if wordData === null && loading}
			<Loader />
			{:else}
			<p class="padding">No result found</p>
			{/if}
		</div>
		{/if}
	</div>
</main>

<style lang="scss">
	@import './styles/app.styles.scss';
</style>