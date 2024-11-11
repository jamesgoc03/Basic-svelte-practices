<script lang="ts">
	import Header from './Header.svelte';
    import { fly } from 'svelte/transition';
	import '../app.css';

	let step: number = $state(0);
	let canContinue: boolean = $state(true);
	let person = $state({
		name: '',
		age: 0,
		gender: ''
	});

	function goOn(field: string) {
		if (field == '') {
			canContinue = false;
		} else {
			step++;
			canContinue = true;
		}
	}
</script>

<main>
	<Header name={person.name} />
	<h4>STEP 0{step + 1}</h4>
	{#if step === 0}
		<div
			in:fly={{ y: 50, duration: 1000, opacity: 0}}
		>
			<label for="name">What is your name?</label>
			<input id="name" bind:value={person.name} type="text" placeholder="Your name" />
			<button onclick={() => goOn(person.name)}>Next Step</button>
		</div>
	{:else if step === 1}
		<div
			in:fly={{ y: 50, duration: 1000, opacity: 0 }}
		>
			<label for="age">What is your age?</label>
			<input id="age" bind:value={person.age} type="number" placeholder="Your age" />
			<button
				onclick={() => {
					if (person.age <= 0) {
						canContinue = false;
					} else {
						step++;
						canContinue = true;
					}
				}}>Next Step</button
			>
		</div>
	{:else if step === 2}
		<div
			in:fly={{ y: 50, duration: 1000, opacity: 0}}
		>
			<label for="gender">What is your gender?</label>
			<input id="gender" bind:value={person.gender} type="text" placeholder="Your gender" />
			<button onclick={() => goOn(person.gender)}>Next Step</button>
		</div>
	{/if}
	{#if step > 2}
        <span 
            in:fly={{ y: 50, duration: 1000, opacity: 0, delay: 500}}
        >
            <h2 class="info">Welcome, {person.name}!</h2>
		    <p class="info">Your age is {person.age} and you gender is {person.gender}</p>
        </span>
	{/if}
	{#if !canContinue}
		<p class="error">You need to introduce something.</p>
	{/if}
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
		background-color: #101010;
	}

	div {
		width: 300px;
		height: 250px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		border-radius: 10px;
		background-color: black;
	}

	h4 {
		color: #ffffff;
		margin-bottom: 10px;
		text-align: center;
		position: fixed;
		top: 100px;
		font-size: 18px;
	}

	label {
		align-self: flex-start;
		margin-left: 50px;
		margin-bottom: 5px;
		color: #cccccc;
	}

	input {
		margin-bottom: 20px;
		padding: 10px;
		border-radius: 5px;
		border: none;
		background-color: #ffffff;
		color: #000000;
		width: 200px;
	}

	button {
		padding: 10px 20px;
		border-radius: 5px;
		border: none;
		background-color: #444444;
		color: #ffffff;
		cursor: pointer;
		transition: background-color 0.25s ease-in-out;
		width: 200px;
	}

	button:disabled {
		background-color: #cccccc;
		cursor: not-allowed;
	}

	button:hover {
		background-color: #101010;
	}

	.error {
		color: rgb(136, 9, 9);
		position: fixed;
		bottom: 150px;
	}

	.info {
		color: #ffffff;
		font-size: 20px;
		text-align: center;
		display: block;
	}
</style>
