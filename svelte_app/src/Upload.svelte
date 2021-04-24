<script>
	let files;

	$: if (files) {
		// Note that `files` is of type `FileList`, not an Array:
		// https://developer.mozilla.org/en-US/docs/Web/API/FileList
		console.log(files);

		for (const file of files) {
			console.log(`${file.name}: ${file.size} bytes`);
		}
	}
</script>
<main>   
    <label for="uploadInput">Laden Sie ein Dokument (PDF, PNG):</label>
    <input
        accept="image/png,application/pdf"
        bind:files
        id="uploadInput"
        name="uploadInput"
        type="file"
    />
</main>

{#if files}
	<h2>Datei:</h2>
	{#each Array.from(files) as file}
		<p>{file.name} ({file.size} bytes) </p>
	{/each}
{/if}