<script>
    import { study } from '../stores.js';
	import Input from './Input.svelte';

</script>

{#each Object.entries($study.items) as [itemName, itemObj]}
    <div class="card">
        <div class="title">
            <h2>{itemName}</h2>
            <span on:keyup={() => {}} on:keydown={() => {}} on:click={() => {delete $study.items[itemName]; console.log("delete", itemName)}}>🗑️</span>
        </div>

        <Input
            type="select"
            setValue={(value) => $study.items[itemName]["type"] = value}
            getValue={() => $study.items[itemName]["type"]}
            label="Type"
            options={["info", "radio", "checkbox", "slider", "image", "picslider", "textinput", "countdown"]}
            pattern={/^.*$/}
            explanation="The type of the item."
            errorExplanation="Your input is not a valid string"
        />

        <Input
            type="text"
            setValue={(value) => $study.items[itemName]["title"] = value}
            getValue={() => $study.items[itemName]["title"]}
            label="Title"
            pattern={/^.*$/}
            explanation="The title of the item."
            errorExplanation="Your input is not a valid string"
        />

        <Input
            type="textarea"
            setValue={(value) => $study.items[itemName]["instruction"] = value}
            getValue={() => $study.items[itemName]["instruction"]}
            label="Instruction"
            pattern={/^.*$/m}
            explanation="The instruction for the item."
            errorExplanation="Your input is not a valid string"
        />

        {#if itemObj.type === "radio" || itemObj.type === "checkbox"}
            <Input 
                type="options"
                label="Options" 
                setValue={(value) => {$study.items[itemName]["options"] = value}}
                getValue={() => $study.items[itemName]["options"]}
                explanation={"Options for your " + itemObj.type + " item."}
                errorExplanation="Your options are not valid."
            />
        {/if}

        {#if itemObj.type === "slider" || itemObj.type === "picslider"}
            <Input 
                type="number"
                label="Min Value"
                pattern={/^-?[0-9]+(\.[0-9]+)?$/}
                setValue={(value) => {$study.items[itemName]["min"] = value}}
                getValue={() => $study.items[itemName]["min"]}
                explanation={"Min value for your " + itemObj.type + " item."}
                errorExplanation="Min value should be a number."
            />

            <Input 
                type="number"
                label="Max Value"
                pattern={/^-?[0-9]+(\.[0-9]+)?$/}
                setValue={(value) => {$study.items[itemName]["max"] = value}}
                getValue={() => $study.items[itemName]["max"]}
                explanation={"Max value for your " + itemObj.type + " item."}
                errorExplanation="Max value should be a number."
            />

            <Input 
                type="number"
                label="Step"
                pattern={/(^-?[0-9]+(\.[0-9]+)?$)|(^$)/}
                setValue={(value) => {$study.items[itemName]["step"] = value}}
                getValue={() => $study.items[itemName]["step"]}
                explanation={"Step for your " + itemObj.type + " item."}
                errorExplanation="Step should be a number."
            />
        {/if}

        {#if itemObj.type === "slider"}
            <Input 
                type="boolean"
                label="Initially Hidden?"
                pattern={/^true$|^false$/}
                setValue={(value) => {$study.items[itemName]["initiallyHidden"] = value}}
                getValue={() => $study.items[itemName]["initiallyHidden"]}
                explanation={"If the " + itemObj.type + " item is initially hidden."}
                errorExplanation="The value is not a valid boolean."
            />

            <Input 
                type="boolean"
                label="Width Variable?"
                pattern={/^true$|^false$/}
                setValue={(value) => {$study.items[itemName]["variableWidth"] = value}}
                getValue={() => $study.items[itemName]["variableWidth"]}
                explanation={"If the width of the " + itemObj.type + " item is variable."}
                errorExplanation="The value is not a valid boolean."
            />
        {/if}

        {#if itemObj.type === "image"}
            <Input 
                type="text"
                label="File name"
                pattern={/^.*\.(png|jpg|jpeg)$/}
                setValue={(value) => {$study.items[itemName]["filename"] = value}}
                getValue={() => $study.items[itemName]["filename"]}
                explanation={"Name of your image file"}
                errorExplanation="File name should be string and should end with a valid extension. (png/jpg/jpeg)"
            />

            <Input 
                type="number"
                label="Scale"
                pattern={/^[0-9]+(\.[0-9]+)?$/}
                setValue={(value) => {$study.items[itemName]["scale"] = value}}
                getValue={() => $study.items[itemName]["scale"]}
                explanation={"Scale of your " + itemObj.type + " item."}
                errorExplanation="Scale should be a number."
            />

            <Input 
                type="number"
                label="Width (px)"
                pattern={/^[0-9]+(\.[0-9]+)?$/}
                setValue={(value) => {$study.items[itemName]["width"] = value}}
                getValue={() => $study.items[itemName]["width"]}
                explanation={"Width of your image."}
                errorExplanation="Width should be a number."
            />

            <Input 
                type="number"
                label="Height (px)"
                pattern={/^[0-9]+(\.[0-9]+)?$/}
                setValue={(value) => {$study.items[itemName]["height"] = value}}
                getValue={() => $study.items[itemName]["height"]}
                explanation={"Height of your image."}
                errorExplanation="Height should be a number."
            />
        {/if}
    </div>
{/each}

<style>
    .card {
        padding: 16px;
        border-radius: 8px;
        box-shadow: 0 0 4px #ccc;
        margin-bottom: 1rem;
    }

    .title {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>
