<script lang="ts">
	import { render } from "svelte/server";
    import type { Snippet } from "svelte";
    import Header from "./Header.svelte";
	import { form } from "$app/server";
	import { fly } from "svelte/transition";

    let formState = $state({
        answers: {},
        step: 0,
        error: ''
    })

    $inspect(formState.step);


    const questions =[
        {
            question: "what's your name?",
            id: 'name',
            type: 'text'
        },
        {
            question: "what's your birthday?",
            id: 'bday',
            type: 'date'
        },
        {
            question: "what's your favorite color?",
            id: 'color',
            type: 'color'
        }
    ]


    function nextStep(id: string){
        if(formState.answers[id] !== ""){
            formState.step += 1;
            formState.error = "";
        } else{
            formState.error = "Please fill out the form"
        }
    }

    $effect(() => {
        console.log("Mounted");
        return () => {
            
            console.log("un mounted");
        }
    });

    $effect(() => {
        // would re-run when formSate.step has changed
        // Don't create state based off other state in effect
        // use $derived
        console.log('formState', formState.step);
        return () => {   
            console.log("before formState reruns", formState.step);
        }
    });
</script>

<Header name={formState.answers.name}>
</Header>
<main>
    {#if formState.step >= questions.length}
        <p>Thanks for filling out</p>
    {:else}
        <p>step = {formState.step + 1}</p>
    {/if}
    

    {#each questions as question, index (question.id) }
        {#if formState.step === index}
        <div in:fly={{x: 200, duration: 200, opacity: 0, delay: 200}} 
            out:fly={{x: -200, duration: 200, opacity: 0}}>
            {@render formStep(question)}
        </div>
            
        {/if}
    {/each}

    {#snippet formStep({ question, id, type }: {
        type: string
        id: string
        question: string
    } )}
        <article>
            <div>
                <label for="id">{question}</label>
                <input {type} {id} bind:value={formState.answers[id]} />
            </div>
            <button onclick={() => nextStep()}>Next</button>
        </article>
    {/snippet}

    {#if formState.error}
        <p class="error">{formState.error + 1}</p>
    {/if}
</main>

{JSON.stringify(formState)}

<style>
    div {
    }
    .error{
        color: red;
    }
</style>