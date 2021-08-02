<style>
    input {
        background-color: var(--highlight);

        /* font-weight: 600; */
        font-size: 1em;
        outline: none;
        border: none;
        padding: 0;

        color: var(--light);
        text-align: center;
    }

	.plus {
		width: 2.15em;
		height: 2.15em;
		border-radius: 100%;
		padding: 0.5em;
	}


    img {
		max-width: 100%;
		max-height: 100%;
		object-fit: contain;
	}
</style>

<script>
    export let content;
    export let cb;
    let interactive = false;
    let width = 2;
</script>

{#if !interactive}
<button class="tag plus" on:click={() => interactive = true}>
    <img src="static/plus.png" alt="plus-icon"/>
</button>
{:else}
<div class="tag">
    <input style="width: {width}ch; " bind:value={content} on:change={() => {cb(); interactive = false; width=2;}} on:input={() => width = content.length}>
</div>
{/if}