<script lang="ts">
    let {name, fakeName}: {name: string, fakeName?: string | null} = $props();
</script>



<h1>
    {#if name}
        Hello {name} from Header
        {fakeName}
    {/if}
</h1>

<style>
</style>