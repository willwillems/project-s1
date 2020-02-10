<script>
	import TheModel from './Model.svelte'
	import TheText from './hero.md'
</script>

<style>
</style>

<TheModel></TheModel>
<main>
	<article id="main">
		<h1>Project S1</h1>
		<div class="button-container">
			<a class="button" href="mailto:s1@willwillems.com?subject=S1%20Dev%20Kit&amp;body=You%20could%20leave%20this%20empty%20or%20just%20say%20hi!">I want a dev kit</a>
			<a class="button" href="mailto:s1@willwillems.com?subject=S1%20Finished%20Unit&amp;body=You%20could%20leave%20this%20empty%20or%20just%20say%20hi!">I want a finished unit</a>
		</div>
		{@html TheText}
	</article>
</main>