<script>
    import SvelteMarkdown from "svelte-markdown"
	import { onMount } from 'svelte';
    import { study } from '../stores.js';

    export let label;
    export let pattern = /.*/;
    export let errorExplanation = "";
    export let explanation = "";
    export let setValue;
    export let getValue;
    export let type = "text";
    export let options = [];

    let preview = false;

    let valid = false;

    let value = [];
    let newOption = "New Option";

    onMount(() => {
     value = getValue();

     if (type === "select") {
            pattern = RegExp(options.map(s => "^" + s + "$").join("|"))
     }

     console.log(value)
    })


    $: valid = pattern.test(value);
</script>



<div title={explanation}>
    <h3><span>{label} {#if type === "textarea"}<span class="preview-button" on:click={() => preview = !preview}>{preview ? "[edit]" : "[preview]"}</span> {/if}</span> <span title={valid ? "Perfect!" : errorExplanation}>{valid ? " 🟢" :  " 🔴"}</span></h3>
    {#if type === "text"}
        <input type="text" bind:value={value} on:change={() => setValue(value)} on:keyup={() => setValue(value)}/>
    {/if}
    {#if type === "textarea"}
        {#if !preview}
            <textarea bind:value={value} on:change={() => setValue(value)} on:keyup={() => setValue(value)}/>
        {:else}
            <div class="preview"><SvelteMarkdown source={value} /></div>
        {/if}
    {/if}
    {#if type === "number"}
        <input type="number" bind:value={value} on:change={() => setValue(value)} on:keyup={() => setValue(value)}/>
    {/if}
    {#if type === "date"}
        <input type="date" bind:value={value} on:change={() => setValue(value)} on:keyup={() => setValue(value)}/>
    {/if}
    {#if type === "select"}
        <select bind:value={value} on:change={() => setValue(value)}>
            {#each options as option}
                <option value={option}>{option}</option>
            {/each}
        </select>
    {/if}
    {#if type === "boolean"}
        <select bind:value={value} on:change={() => setValue(value)}>
            {#each [true, false] as option}
                <option value={option}>{option}</option>
            {/each}
        </select>
    {/if}
    {#if type === "options"}
        {#each value as v}
            <span class="option" on:keyup={() => {}} on:click={() => {value = value.filter((x) => x !== v); setValue(value)}}>{v}</span>
        {/each}
        
        <span contenteditable="" placeholder="New Option" on:keypress={(e) => {if (e.key === "Enter") {e.preventDefault(); value.push(newOption); setValue(value); newOption = "New Option"; value = value}}} bind:innerText={newOption} class="new-option"></span>

    {/if}

    
</div>


<style>
    div {
        margin: 1rem 0;
    }
    h3 {
        margin-bottom: 0.5rem;
        display: flex;
        justify-content: space-between;
    }

    input, select {
        width: 100%;
    }

    input, select {
        font-family: 'Lato', -apple-system, BlinkMacSystemFont, Segoe UI, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
        background-color: #efefef;
        border: none;
        border-radius: 8px;
        padding: 4px 8px;
        box-sizing: border-box;
        font-size: larger;
    }

    textarea {
        font-family: 'Lato', -apple-system, BlinkMacSystemFont, Segoe UI, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
        background-color: #efefef;
        border: none;
        border-radius: 8px;
        width: 100%;
        height: 100px;
        padding: 4px 8px;
        box-sizing: border-box;
        font-size: larger;
    }

    .preview {
        background-color: #efefef;
        border-radius: 8px;
        padding: 4px 8px;
    }

    .preview-button {
        color: gray;
        cursor: pointer;
    }

    .option {
        padding: 0.25rem 0.5rem;
        margin-right: 0.25rem;
        margin-bottom: 1rem;
        border-radius: 99px;
        background-color: #efefef;
        white-space: nowrap;
        cursor: pointer;
    }

    .option:hover {
        text-decoration: line-through;
        background-color: lightcoral;
    }

    .new-option {
        padding: 0.25rem 0.5rem;
        margin-right: 0.25rem;
        margin-bottom: 1rem;
        border-radius: 99px;
        background-color: #efefef;
        white-space: nowrap;
        background: none;
        border: 1px solid lightgray;
    }

    .sub {
        color: gray;
        margin: 0;
        font-style: italic;
    }
</style>