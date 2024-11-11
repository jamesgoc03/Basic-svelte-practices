<script lang="ts">
    let {name}: {name: string} = $props();
</script>



<h1 class="fixed top-0 w-full h-16 bg-black text-white">
    {#if name}
        Hello, {name}! This is your form 
    {:else} 
        Hello, Stranger! This is your form
    {/if}
</h1>

<style>
    h1 {
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: bolder;
        font-size: 25px;
    }
</style>