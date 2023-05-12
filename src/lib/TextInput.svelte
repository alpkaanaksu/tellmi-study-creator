<script>
    export let label;
    export let setValue;

    let value = "";
</script>

<input type="text" bind:value={value} on:change={setValue(value)}/>