<script>
    import Character from "./lib/Character.svelte";

    let characters = [];
    let page = 1;

    async function loadCharacters() {
        const response = await fetch('https://rickandmortyapi.com/api/character?page=' + page);
        const data = await response.json();
        characters = data.results;
    }

    function nextPage() {
        page++;
        loadCharacters();
    }

    function previousPage() {
        page--;
        loadCharacters();
    }

    loadCharacters();
</script>

<main>
    <h1 class="title">
        Rick and Morty Frontend API
    </h1>

    <div class="buttons">
        <button class="button" onclick={previousPage} disabled={page === 1}>Previous</button>
        <span class="button number">{page}</span>
        <button class="button" onclick={nextPage} disabled={page === 42}>Next</button>
    </div>
    <div class="container">
        <div class="grid">
            {#each characters as character}
                <Character {character} />
            {/each}
        </div>
    </div>
</main>

<style>
</style>
