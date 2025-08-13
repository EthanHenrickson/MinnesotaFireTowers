<script lang="ts">
	import firetower from '$lib/assets/firetower.png';
	import Nav from '$lib/components/Nav.svelte';
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={firetower} />
</svelte:head>

<Nav />
<div class="content">
	{@render children?.()}
</div>

<style>

	.content {
		padding-top: 3rem;

		max-width: 1000px;
		margin-left: auto;
		margin-right: auto;
		padding-left: 1rem;
		padding-right: 1rem;
		
	}

	:global(:root) {
		--AccentColorPrimary: #00a62f;
		--AccentColorSecondary: #d5f7d4;
		--AccentColorTertiary: #f8f9fa;

		--text-color: black;
	}

	:global(html) {
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		background-color: #fcfef6;
	}

	:global(h1) {
		font-size: 2rem;
		margin-bottom: 1.5rem;
	}

	:global(h2) {
		font-size: 1.5rem;
		margin: 2rem 0 1rem;
	}

	:global(ul) {
		margin: 1rem 0;
		padding-left: 2rem;
	}

	:global(li) {
		margin-bottom: 0.5rem;
	}

	:global(strong) {
		font-weight: bold;
	}

	:global(a) {
		font-size: 1.2rem;
	}

	:global(p) {
		margin: 0.8rem 0px;
	}

	:global(button) {
		padding: 0.7rem 1.5rem;
		background-color: var(--AccentColorPrimary);
		color: white;
		border-radius: 0.4rem;
		cursor: pointer;
		border: none;
		font-size: 0.9rem;
	}

	:global(button:focus-visible, a:focus-visible, input:focus-visible, select:focus-visible) {
		outline: 2px solid var(--AccentColorPrimary) !important;
		outline-offset: 2px;
		border-radius: 0.25rem;
	}

	:global(select) {
		padding: 0.2rem 0.7rem;
		font-size: 0.9rem;

		outline: none;
		background-color: transparent;

		border-bottom: 2px solid var(--AccentColorPrimary);
		border-top: none;
		border-right: none;
		border-left: none;
	}

	:global(input[type='checkbox']) {
		accent-color: var(--AccentColorPrimary);
	}
</style>
