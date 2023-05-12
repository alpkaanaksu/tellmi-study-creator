<script>
    import { study } from "../stores";

    let json = JSON.stringify($study, null, 2);

    let copied = false;
    let blob = new Blob([json], { type: "text/json;charset=utf-8" });
    let filename = `variant_${$study.settings["study.variant"]}.json`;
</script>

<a download={filename} href={(window.URL || window.webkitURL).createObjectURL(blob)}>Download <b>{filename}</b></a>

<span on:click={() => { navigator.clipboard.writeText(json); copied = true;}}>Copy JSON to clipboard {copied ? "✅" : ""}</span>

<style>
    a, span {
        background-color: #efefef;
        padding: 0.25rem 0.5rem;
        border-radius: 99px;
        cursor: pointer;
    }
</style>

