<script>
    import Field from "../components/Field.svelte";
    import Tag from "../components/Tag.svelte";
    import CreateTag from "../components/CreateTag.svelte";

    let stepDescription = "Wähle dein Thema!"
    let fieldTitle = "Thema"
    let fieldDescription = "Hier wird dein Thema eingefügt!"
    let tags = ["Mobility", "Sustainability"]

    let maxAmount = 2
    let selected = [null]
	let newtag = ""

    function select(name) {
        if (selected.length == 1 && selected[0] === null)
            selected.pop()

        if (selected.indexOf(name) === -1 && selected.length >= maxAmount)
            selected.pop()
        toggle(name)

        if (selected.length == 0) {
            selected.push(null)
        }

        console.log(selected)
        // to trigger update
        selected = selected
    }

    function toggle(value) {
        if (selected.indexOf(value) !== -1) {
            selected.splice(selected.indexOf(value), 1)
        }
        else {
            selected.push(value)
        }
    }
</script>

<div class="step-container">
    <div class="section f2">
        <h1 class="step">{stepDescription}</h1>
    </div>
    <div class="section f2">
        <div class="field-collection">
            {#each selected as element, i}
                <Field fieldTitle={selected.length > 1 ? fieldTitle + ' ' + (i + 1) : fieldTitle} fieldDescription={fieldDescription} fieldValue={element}/>
            {/each}
        </div>
    </div>
    <div class="section f3">
        <div class="tag-collection">
            {#each tags as tag}
                <Tag content={tag} selected={selected.includes(tag)} on:click={() => select(tag)}/>
            {/each}
            <CreateTag cb={() => {console.log("push"); tags = [...tags, newtag]; newtag = "";}} bind:content={newtag}/>
        </div>
    </div>
</div>

<style>
	:global(:root) {
		--dark: #202231;
		--light: #edf2f4;
		--highlight: #0aa77e;
	}

	:global(html) {
		background-color: var(--dark);
	}

    :global(body) {
        margin: 0;
    }

	.step-container {
		height: 100vh;
		margin: 0;

		display: flex;
		flex-direction: column;
		justify-content: space-between;

		color: var(--light);
		font-family: sans-serif;
	}

	.section {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.f1 {
		flex: 1;
	}

	.f2 {
		flex: 2;
	}

	.f3 {
		flex: 3;
	}

	.step {
		font-size: 1.3em;
	}

	.field-collection {
		width: 80%;
		display: flex;
		flex-direction: row;

		justify-content: space-evenly;
	}
	.tag-collection {
		width: 80%;
		display: flex;

		flex-direction: row;
		align-items: center;
		justify-content: center;
	}

	:global(.tag) {
		background-color: var(--highlight);

		/* font-weight: 600; */
		font-size: 1.3em;

		padding: 0.5em 0.7em;
		border-radius: 100px;
		margin: 0em 0.5em;

		border: none;
		color: var(--light);
	}
</style>
