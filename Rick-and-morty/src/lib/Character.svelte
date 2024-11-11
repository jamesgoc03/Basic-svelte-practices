<script lang="ts">
    interface Character {
        name: string;
        species: string;
        image: string;
    }
    let {character}: {character: Character} = $props();  
</script>

<div class="character">
    <img src={character.image} alt={character.name} />
    <h2> {character.name} </h2>
    <h3> {character.species} </h3>
</div>