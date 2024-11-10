<script>
  import Input from "./lib/Input.svelte";
  import Dropdown from "./lib/Dropdown.svelte";
  import Ranks from "./lib/Ranks.svelte";


  let state = {
    name: "Joe",
    lastname: "Doe",
    sector: "Frontend",
    salary: {
      min: 25000,
      max: 45000
    }
  }

  let error = null;

  let sectors = ["Backend", "Frontend", "Devops", "QA"]

  function sent(event) {
    event.preventDefault();
    alert(JSON.stringify(state));
  }

  function updateSalary(event) {
    state.salary.min = event.detail.min;
    state.salary.max = event.detail.max;
    if(state.salary.min > state.salary.max)
      error = "The minimum value cannot be greater than the maximum value.";
    else 
      error = null;
  }
</script>

<main>
  <form on:submit={sent}>
    <Input identifier="name" label="Name" bind:value={state.name}/>
    <Input identifier="lastname" label="Lastname" bind:value={state.lastname}/>
    <Dropdown identifier="sector" label="Sector" choises={sectors} bind:value={state.sector}/>
    <Ranks identifier="salary" label="Salary" min={state.salary.min} max={state.salary.max} on:update={updateSalary}/>
    {#if error != null}
      <p>{error}</p>
    {/if}
    <p>
      <input type="submit" value="send" disabled={error != null}>
    </p>
  </form>
</main>

<style>
</style>
