<script lang="ts">
    import { error } from "@sveltejs/kit";
import Header from "./Header.svelte"

    let name: string = $state("John");
    let status: "open" | "closed" = $state("open")
    let fullName = $derived(name + " " + "last name");
    let formState = $state({
        name: "",
        birthday: "",
        step: 0,
        error: ""
    })

    function toggle() {
        status = status === "open" ? "closed" : "open";
    }
</script>

<Header {name} />
<h2>Hello again {fullName}</h2>
<input type="text" bind:value={name}>

<p>The store is now {status}</p>
<button onclick={toggle}>Toggle status</button>
<button onclick={() => {
    status = status === "open" ? "closed" : "open";
}}>Toggle status</button>

<main>
    <p>Step: {formState.step}</p>
    {@render formStep({question: "What is your name?", id: "name", type: "text"})}

    {#if formState.step === 0}
        <div>
            <label for="name">Your name</label>
            <input type="text" id="name" bind:value={formState.name}>
            <button onclick={() => {
                if(formState.name !== "") {
                    formState.step += 1;
                    formState.error = "";
                } else {
                    formState.error = "Your name is Empty. Please write your name";
                }    
            }}>Next</button>
        </div>
    {:else if formState.step == 1}
        <div>
            <label for="birth">Your birthday</label>
            <input type="text" id="birth" bind:value={formState.birthday}>
            <button onclick={() => {
                if(formState.birthday !== "") {
                    formState.step += 1;
                    formState.error = "";
                } else {
                    formState.error = "Your birthday is Empty. Please write your birthday";
                }    
            }}>Next</button>
        </div> 
    {/if}
    {#if formState.error}
        <p class="error">{formState.error}</p>
    {/if}
</main>


{#snippet formStep({question, id, type}: 
                   {question:string, id:string, type:string})}
    <article>
        <div>
            <label for={id}>{question}</label>
            <input type={type} id={id} bind:value={formState[id]}>
        </div>
    </article>
{/snippet}


<style>
    .error {
        color: red;
    }
</style>