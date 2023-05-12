<script>
    import { study } from '../stores.js';

	import Input from "./Input.svelte";
</script>

<Input
    type="text"
    setValue={(value) => $study.settings["study.name"] = value}
    getValue={() => $study.settings["study.name"]}
    label="Study Name"
    pattern={/^.*$/}
    explanation="You can have different conditions in a study."
    errorExplanation="Your input is not a valid string"
/>

<hr>

<Input
    type="text"
    setValue={(value) => $study.settings["study.id"] = value}
    getValue={() => $study.settings["study.id"]}
    label="Study ID"
    pattern={/^[A-Z]{3}$/}
    explanation="The ID of your study. It should be unique and consist of 3 uppercase letters."
    errorExplanation="Your input does not consist of exactly 3 uppercase letters."
/>

<hr>

<Input
    type="text"
    setValue={(value) => $study.settings["study.variant"] = value}
    getValue={() => $study.settings["study.variant"]}
    label="Study Variant"
    pattern={/^[A-Z]{2}$/}
    explanation="You can have different conditions in a study."
    errorExplanation="Your input does not consist of exactly 2 uppercase letters."
/>

<hr>

<Input
    type="select"
    setValue={(value) => $study.settings["start"] = value}
    getValue={() => $study.settings["start"]}
    label="Start"
    options={["relative", "fixed", "user", "nextWeekDay"]}
    pattern={/^relative$|^fixed$|^user$|^nextWeekDay$/}
    explanation="Start of the study"
    errorExplanation="Your input does not match one of the given options."
/>

<hr>

<Input
    type="number"
    setValue={(value) => $study.settings["start.day"] = value}
    getValue={() => $study.settings["start.day"]}
    label="Start Day"
    pattern={/^[0-9]+$/}
    explanation="First day of the study, related to the 'Start' parameter"
    errorExplanation="Your input is not a number."
/>

<hr>

<Input
    type="date"
    setValue={(value) => $study.settings["start.date"] = value}
    getValue={() => $study.settings["start.date"]}
    label="Start Date"
    pattern={/^[0-9]{4}-[0-9]{2}-[0-9]{2}$/}
    explanation="Start date of the study"
    errorExplanation="Your input is not a valid date."
/>

<hr>

<Input
    type="number"
    setValue={(value) => $study.settings["start.shift"] = value}
    getValue={() => $study.settings["start.shift"]}
    label="Start Shift"
    pattern={/^[0-9]+$/}
    explanation="Start shift of the study"
    errorExplanation="Your input is not a valid number"
/>

<hr>

<Input
    type="date"
    setValue={(value) => $study.settings["start.final"] = value}
    getValue={() => $study.settings["start.final"]}
    label="Last day to start the study"
    pattern={/^[0-9]{4}-[0-9]{2}-[0-9]{2}$/}
    explanation="Last start date of the study"
    errorExplanation="Your input is not a valid date."
/>

<hr>

<Input
    type="text"
    setValue={(value) => $study.settings["study.admin.name"] = value}
    getValue={() => $study.settings["study.admin.name"]}
    label="Name of the study admin"
    pattern={/^.*$/}
    explanation="Name of the study admin."
    errorExplanation="Your input is not a valid string"
/>

<hr>

<Input
    type="text"
    setValue={(value) => $study.settings["study.admin.email"] = value}
    getValue={() => $study.settings["study.admin.email"]}
    label="Name of the study admin"
    pattern={/^.*@.*\..*$/}
    explanation="Name of the study admin."
    errorExplanation="Your input is not a valid string"
/>

<hr>

<Input
    type="boolean"
    setValue={(value) => $study.settings["online"] = value}
    getValue={() => $study.settings["online"]}
    label="Online"
    pattern={/^true$|^false$/}
    explanation="Online?"
    errorExplanation="Your input is not a valid boolean value"
/>

<style>
    hr {
        border: 0;
        height: 0;
        border-top: 1px solid rgba(0, 0, 0, 0.1);
        border-bottom: 1px solid rgba(255, 255, 255, 0.3);border-top: 1px solid lightgray;
    }
</style>