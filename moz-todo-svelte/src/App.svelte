<script>
	export let start;
	import Upload from './Upload.svelte';

	function toggleStart() {
    if (start != true) {
      start = true;
    }
  }
</script>

<main>
	<h2>DigiTecten</h2>
	<h1>Amazing Tagger Tool - DigiDecten</h1>	
	<div class="pure-g">
		<div class="pure-u-1-3"></div>
		<div class="pure-u-1-3">
			
			<p>Laden Sie ihren Bauplan als PDF, markieren Sie ein Element und sehen Sie die dazugehörigen Elemente</p>
			<button on:click={toggleStart}>Start</button>
			{#if start}
				<Upload/>
			{/if}
		</div>
		<div class="pure-u-1-3"></div>
	</div>
</main>

<style>
	:global(main) {
		text-align: center;
		padding: 1em;
		/*max-width: 240px;*/
		margin: 0 auto;
		background-color: rgba(220, 229, 241, 0.95);
		padding-bottom: 100px;
	}
	
	h1 {
		color:deepskyblue;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 200;
		margin-top: 0;
	}
	h2 {
		color:rgb(236, 153, 0);
		font-size: 1.5em;
		font-weight: 300;
		margin: 10;
		margin-bottom: 0;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

