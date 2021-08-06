<script>
    export let content = " ";
    export let selected = false;
    export let deletecb;
</script>

<style>
    .selected {
		border: 2px solid var(--light);
	}

    :global(.tag) {
        position: relative;
		background-color: var(--highlight);

		/* font-weight: 600; */
		font-size: 1.3em;

		padding: 0.5em 0.7em;
		border-radius: 100px;
		margin: 0em 0.5em;

		border: none;
		color: var(--light);
	}

    .tag .rm-button {
        display: none;
    }

    .tag:hover .rm-button {
        display: block;
    }

    .rm-button {
        display: none;
        position: absolute;
        top: 0;
        right: 0;

        width: 1.5em;
        height: 1.5em;

        border-radius: 1em;
        border: .2em var(--light) solid;
        outline: none;

        background-color: var(--highlight);
        color: var(--light);
        padding: 0px;
    }

    .rm-button > img {
        transform: rotate(45deg);
        max-width: 70%;
        max-height: 70%;
        object-fit: contain;

        /* for the img inside your div */
        display: block;
        margin: auto;
        pointer-events: none;
    }
</style>

<button class="tag {selected ? "selected" : ""}" on:click|self on:contextmenu>
    {content}
    <button class="rm-button" on:click|self={deletecb()}><img src="static/plus.png" alt="remove-icon"/></button>
</button>