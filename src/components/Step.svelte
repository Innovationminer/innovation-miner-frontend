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

	.next {
		background-color: transparent;
		border: none;

		color: var(--light);
		font-size: 3em;
	}

	.last-step-result {
		font-size: 2.5em;
		/* TODO: font richtig importieren */
		font-weight: thin;
	}

	.hide {
		display: none;
	}
</style>

<script>
    import Field from "../components/Field.svelte";
    import Tag from "../components/Tag.svelte";
    import CreateTag from "../components/CreateTag.svelte";
	//
	import Fa from 'svelte-fa'
  	import { faArrowDown } from '@fortawesome/free-solid-svg-icons'
	//

    export let stepDescription = "Wähle dein Thema!"
    export let fieldTitle = "Thema"
    export let fieldDescription = "Hier wird dein Thema eingefügt!"
    export let tags = ["Mobility", "Sustainability"]

    export let maxAmount = 2
    let selected = [null]
	let newtag = ""

	export let nextPagecb;


	function handleSelection(value) {
        if (selected.length == 1 && selected[0] === null)
            selected.pop()

        if (selected.indexOf(value) === -1 && selected.length >= maxAmount)
            selected.pop()

        toggle(value)

        if (selected.length == 0) {
            selected = add(selected, null)
        }
	}

    function select(value) {
		selected = add(selected, value)
    }

	function unselect(value) {
        selected = remove(selected, value)
	}

    function toggle(value) {
        if (selected.indexOf(value) !== -1)
            unselect(value)
        else
            select(value)
    }

	function removeTag(tag) {
		if (selected.indexOf(tag) !== -1){
			toggle(tag)
			selected.push(null)
		}

        tags = remove(tags, tag)
		selected = selected;
	}

	function remove(array, value) {
		console.log("Remove", value, "from", array)
		if (array.indexOf(value) !== -1) {
            array.splice(array.indexOf(value), 1)
		}
		return array
	}

	function add(array, value) {
		console.log("Add", value, "to", array); 
		array = [...array, value];
		return array
	}

	function addNewTag() {
		tags = add(tags, newtag);
		newtag=""
	}
</script>

<div class="step-container">
	<div class="section f1">
		<div class="last-step-result">
			Last step result
		</div>
	</div>
    <div class="section f2">
        <h1 class="step">{stepDescription}</h1>
    </div>
    <div class="section f3">
        <div class="field-collection">
            {#each selected as element, i}
                <Field fieldTitle={selected.length > 1 ? fieldTitle + ' ' + (i + 1) : fieldTitle} fieldDescription={fieldDescription} fieldValue={element}/>
            {/each}
        </div>
    </div>
    <div class="section f3">
        <div class="tag-collection">
            {#each tags as tag}
                <Tag content={tag} selected={selected.includes(tag)} on:click={() => handleSelection(tag)} deletecb={() => removeTag(tag)}/>
            {/each}
            <CreateTag cb={addNewTag} bind:content={newtag}/>
        </div>
    </div>
	<div class="section f1">
		<button class="next {selected[0] != undefined ? "" : "hide"}" on:click={nextPagecb(selected)}>
			<Fa icon={faArrowDown} />
		</button>
	</div>
</div>
