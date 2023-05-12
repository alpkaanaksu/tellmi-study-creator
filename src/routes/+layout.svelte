<script>
	import Header from "../lib/Header.svelte";
    import "../global.css"

</script>

<Header></Header>
<div></div>
<slot></slot>

<style>
    div {
        margin-bottom: 5rem;
    }
</style>