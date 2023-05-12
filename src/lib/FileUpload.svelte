<script>
    import { study } from '../stores.js';

    
    let files;

    const handleChange = async () => {
        $study = JSON.parse(await files[0].text());
    }
    
</script>

<div>
    <p>Open your JSON file</p>

    <input
        accept="text/json"
        bind:files
        id="study"
        name="study"
        type="file"
        on:change={handleChange}
    />

    <p><i>or</i><br>start with a Tellmi study template.</p>
</div>

<style>
    i {
        color: gray;
    }

    div {
        font-size: larger;
    }
</style>