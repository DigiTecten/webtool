<script>
	import Tagger from './Tagger.svelte';
	let files,
		uploadFile,
		predictions;

	$: if (files) {
		// Note that `files` is of type `FileList`, not an Array:
		// https://developer.mozilla.org/en-US/docs/Web/API/FileList
		console.log(files);

		for (const file of files) {
			console.log(`${file.name}: ${file.size} bytes`);
		}
	}
	async function doPost () {
		const res = await fetch('http://localhost:8080/postFile', {
			method: 'POST',
			body: JSON.stringify({
				foo,
				bar
			})
		})
		
		const json = await res.json()
		result = JSON.stringify(json)
		console.log('result:', result);
	}

	function upload() {
		if (files) {
			const formData = new FormData();
			formData.append('dataFile', files.item(0));
			const upload = fetch('http://localhost:8080/upload', {
				method: 'POST',
				body: formData
			}).then((response) => response.json()).then((result) => {
				console.log('Success:', result.message);
				predictions = result.prediction;
				uploadFile = result.name.replace('.pdf', '-1.png');
			})
			.catch((error) => {
				console.error('Error:', error);
			});
		}
    }
	
</script>
{#if !uploadFile}
	<main>   
		<label for="uploadInput">Laden Sie ein Dokument (PDF, PNG):</label>
		<input
			accept="image/png,application/pdf"
			bind:files
			id="uploadInput"
			name="uploadInput"
			type="file"
		/>
		<button on:click={upload}>Laden</button>
	</main>

	{#if files}
		<h2>Datei:</h2>
		{#each Array.from(files) as file}
			<p>{file.name} ({file.size} bytes) </p>
		{/each}
	{/if}
{/if}
{#if uploadFile}
	<p>Bauplan taggen:</p>
	<div id="tagger">
		<img src="http://localhost:8080/static/{uploadFile}"/>
		{#each predictions as prediction}
			<div class="prediction" style="top: {prediction.top}px; left: {prediction.left}px; width: {prediction.left2-prediction.left}px; height: {prediction.top2 - prediction.top}px;"></div>
		{/each}
	</div>	
{/if}
<style>
	#tagger {
		width: 99%;
		margin: 0;
		overflow: auto;
		position: relative;
	}

	.prediction {
		z-index: 1;
		background-color: rgba(255, 0, 0, 0.5);
		position: absolute;
	}
</style>
