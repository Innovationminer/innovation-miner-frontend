<script>
	import Step from "../components/Step.svelte";

	let steps = [{
		stepDescription: "Wähle dein Thema!",
		fieldTitle: "Thema",
		fieldDescription: "Hier wird dein Thema eingefügt!",
		tags: ["Mobility", "Sustainability"],
		maxAmount: 1
	},{
		stepDescription: "Wähle dein Thema 2!",
		fieldTitle: "Thema 2",
		fieldDescription: "Hier wird dein Thema 2 eingefügt!",
		tags: ["Mobility", "Sustainability"],
		maxAmount: 2
	},{
		stepDescription: "Wähle dein Thema 3!",
		fieldTitle: "Thema 3",
		fieldDescription: "Hier wird dein Thema 3 eingefügt!",
		tags: ["Mobility", "Sustainability", "Crap"],
		maxAmount: 3
	}
	];

	let lastResult = "";
	let currentStepIdx = 0;
	let currentStep = steps[currentStepIdx];

	function nextPage(result) {
		console.log(result)
		lastResult = result;

		if (currentStepIdx + 1 >= steps.length){
			console.log("Finished all steps")
			return
		}

		currentStepIdx = currentStepIdx + 1;
		currentStep = steps[currentStepIdx]

		console.log(currentStep)
	}
</script>

{#key currentStep}
	<Step {...currentStep} nextPagecb={nextPage}/>
{/key}