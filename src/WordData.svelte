<script>
    export let wordData = null;

    const playAudio = (src) => {
        let audio = new Audio(src);
        audio.play();
    }
</script>

<div class="word-data">
    {#if wordData.phonetics}
    <div class="audios">
        {#each wordData.phonetics as data}
        <div class="audio">
            {#if data.text}
            <p>
                {data.text}
                {#if data.audio}
                <i class="fa fa-play-circle" on:click={() => playAudio(data.audio) }></i>
                {/if}
            </p>
            {/if}
        </div>
        {/each}
    </div>
    {/if}
    {#each wordData.meanings as meaning}
        <div class="meaning">
            <div class="part-of-speech">&bull; {meaning.partOfSpeech}</div>
            <div class="definitions">
                {#each meaning.definitions as data}
                    <div class="definition">
                        <p>Definition: <b>{data.definition}</b></p>
                        {#if data.example}
                            <p>Example: <i>{data.example}</i></p>
                        {/if}
                    </div>
                {/each}
            </div>
        </div>
    {/each}
</div>

<style lang="scss">
    @import './styles/word-data.styles.scss';
</style>