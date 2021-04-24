<script>
	export let name;
	import Upload from './Upload.svelte';

	function toggleName() {
    if (name === 'world') {
      name = 'svelte'
    } else {
      name = 'world'
    }
  }
</script>

<main>
	<h1>Hello {name}!</h1>
	<button on:click={toggleName}>Toggle name</button>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
	:global(main) {
		text-align: center;
		padding: 1em;
		/*max-width: 240px;*/
		margin: 0 auto;
		background-color: #bccce2;
	}

	h1 {
		color:deepskyblue;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

<Upload/>