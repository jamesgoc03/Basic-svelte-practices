<script>
    export let identifier;
    export let label;
    export let choises;
    export let value;
</script>

<p>
    <label for={identifier}>{label}</label>
    <select id={identifier} bind:value>
        {#each choises as choise}
            <option value={choise}>{choise}</option>
        {/each}
    </select>
</p>