<script>
    import { study, page } from '../stores.js';

	import FileUpload from "./FileUpload.svelte";
    import Items from "./Items.svelte"
	import Save from './Save.svelte';
	import StudySettings from './StudySettings.svelte';

</script>


<div>
    {#if !$study.settings}
        <FileUpload/>
    {:else}
        {#if $page === "settings"}
            <h1>Study Settings</h1>
            <StudySettings />
        {:else if $page === "items"}
            <h1>Items</h1>
            <Items />
        {:else if $page === "sets"}
            <h1>Sets</h1>
        {:else if $page === "schedule"}
            <h1>Schedule</h1>
        {:else if $page === "images"}
            <h1>Images</h1>
        {:else if $page === "save"}
            <h1>Save</h1>
            <Save />
            <pre>{JSON.stringify($study, null, 2)}</pre>

        {/if}
    {/if}
</div>

<style>
    div {
        width: 90%;
        max-width: 640px;
        margin: 0 auto;
    }
</style>