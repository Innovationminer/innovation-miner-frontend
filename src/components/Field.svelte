<script>
    export let fieldTitle;
    export let fieldDescription;
    export let fieldValue;
</script>

<div class="field-container">
    {#if fieldValue == null}
	<h2 class="title la">{fieldTitle}</h2>
	<div class="field">
        {fieldDescription}
    </div>
    {:else}
	<h2 class="title ca">{fieldTitle}</h2>
	<div class="selected-field">
        {fieldValue}
    </div>
    {/if}
</div>

<style>
    .title {
    	margin: 0;
		font-weight: normal;
	}

	.la {
        text-align: start;
	}

    :global(.ca) {
        text-align: center;
	}

	.field {
		border: 1px dashed var(--light);

		padding: 6em 6em;
	}

    .selected-field {
		padding: 0.2em 0em;
        font-size: 3.5em;
        font-weight: bold;
    }
</style>
