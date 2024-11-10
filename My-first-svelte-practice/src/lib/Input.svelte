<script>
    export let identifier;
    export let value;
    export let label;
</script>

<p>
    <label for={identifier}>{label}</label>
    <input id={identifier} type="text" bind:value>
</p>