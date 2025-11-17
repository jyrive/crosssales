<script>
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Cross-Sales Insurance Prototype</title>
</svelte:head>

<main class="min-h-screen bg-nordic-50">
	{@render children()}
</main>
