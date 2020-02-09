<script>
	import TheModel from './Model.svelte'
	import TheText from './hero.md'
</script>

<style>
</style>

<TheModel></TheModel>
<main>
	<article id="main">
		{@html TheText}
	</article>
</main>