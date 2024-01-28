<script>
	import { onMount } from "svelte";
	let inputValue = "";
	let outputValue = "";
	$: resultBoxColor = "";
	async function handleInput(event) {
		inputValue = event.target.inputValue;
		//	await callAPI(inputValue);
	}

	async function callAPI(text) {
		console.log(text);
	}

	async function submitForm(event) {
		event.preventDefault();
		console.log("Form submitted", inputValue);
		const endpoint = "http://localhost:3000/";
		const requestBody = {
			color: inputValue,
		};
		const requestOptions = {
			method: "POST",
			headers: {
				"content-type": "application/json",
			},
			body: JSON.stringify(requestBody),
		};
		await fetch(endpoint, requestOptions)
			.then((res) => res.json())
			.then((data) => {
				outputValue = data["name"];
				console.log(outputValue);
				resultBoxColor = outputValue;
				console.log(resultBoxColor);
			})
			.catch((error) => console.log("Error while fetching", error));
	}

	
</script>

<main>
	<form on:submit={submitForm}>
		<div class="input-box">
			<p>ENTER THE COLOR</p>
			<input type="text" bind:value={inputValue} />
		</div>
	</form>

	<form on:submit={submitForm}>
		<div class="input-box">
			<p>RESULT TEXT</p>
			<input class="result-box" type="text" bind:value={outputValue} style="color:{resultBoxColor}" />
		</div>
	</form>

	<!-- <style>
		.result-box {
			color: var(--resultBoxColor, grey) !important;
		} 
	</style> -->
</main>
