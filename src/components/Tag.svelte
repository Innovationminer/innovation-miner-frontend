<script>
    export let content;
    export let selected;
</script>

<style>
    .selected {
		border: 2px solid var(--light);
	}
</style>

<button class="tag {selected ? "selected" : ""}" on:click>
    {content}
</button>