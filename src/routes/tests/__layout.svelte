<svelte:head>
	<title>KGC - Test</title>
</svelte:head>

<main>
	<slot />
</main>

<footer>
	<div class="copyright">copyright 2022</div>
</footer>

<style>
	footer {
		padding: 40px;
		text-align: center;
	}
	.copyright {
		color: #aaa;
		font-size: 14px;
		display: inline-block;
		padding: 20px;
		border-top: 1px solid #ddd;
	}
</style>
