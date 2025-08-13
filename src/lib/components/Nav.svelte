<script lang="ts">
	import { page } from '$app/state';
	import Close from '$lib/assets/icons/close.svelte';
	import Menu from '$lib/assets/icons/menu.svelte';

	let isMobile = $state(false);
	let isOpen = $state(false);

	let windowWidth: number = $state(0);
	$effect(() => {
		//Check if we are under 600px and should be in mobile mode
		isMobile = windowWidth < 600;

		//Close menu if we aren't in mobile mode
		if (!isMobile) {
			isOpen = false;
		}
	});

	function toggleMenu() {
		isOpen = !isOpen;
	}
</script>

<svelte:window bind:innerWidth={windowWidth} />

<header>
	<div class="header">
		<a class="logo" href="/">Minnesota Fire Towers</a>

		<span class="gap"></span>

		{#if isMobile}
			<button
				onclick={toggleMenu}
				aria-label={isOpen ? 'Close menu' : 'Open menu'}
				aria-expanded={isOpen}
				aria-haspopup="true"
				class="menu-toggle"
			>
				{#if isOpen}
					<Close />
				{:else}
					<Menu />
				{/if}
			</button>
		{/if}

		<nav class="mainNav" class:open={isOpen} aria-label="Main">
			<div class="nav-links">
				<a
					href="/"
					onclick={toggleMenu}
					class:active={page.url.pathname === '/'}
					aria-current={page.url.pathname === '/' ? 'page' : undefined}>Home</a
				>
				<a
					href="/chat"
					onclick={toggleMenu}
					class:active={page.url.pathname === '/towers'}
					aria-current={page.url.pathname === '/towers' ? 'page' : undefined}>Towers</a
				>
				<a
					href="/login"
					onclick={toggleMenu}
					class:active={page.url.pathname === '/map'}
					aria-current={page.url.pathname === '/map' ? 'page' : undefined}>Map</a
				>
			</div>
		</nav>
	</div>
</header>

<style>
	.header {
		height: var(--header-height);
		padding: 0 2rem;
		display: flex;
		align-items: center;
		border-bottom: 1px solid var(--hover-bg);

		position: fixed;
		top: 0;
		left: 0;
		right: 0;

		z-index: 100;
		padding: 10px 4rem;
		background-color: var(--AccentColorSecondary);
	}

	.logo {
		font-size: 1.6rem;
		font-weight: 400;
		color: var(--primary-color);
		z-index: 101;
		padding: 0.25rem;

		text-decoration: none;
	}

	.mainNav {
		display: flex;
		gap: 2rem;
		align-items: center;
	}

	.mainNav a {
		text-decoration: none;
		color: var(--text-color);
		font-size: 1.1rem;
		transition: color 0.2s;
		font-weight: 400;
	}

	.menu-toggle {
		background: none;
		border: none;
		cursor: pointer;
		padding: 0.5rem;
		z-index: 1000;
	}

	.mainNav a.active {
		text-decoration: underline;
		text-decoration-thickness: 2px;
		text-decoration-color: var(--AccentColorPrimary);
	}

	.nav-links {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		height: 100%;
		gap: 2rem;
	}

	.gap {
		flex-grow: 2;
	}

	@media (max-width: 600px) {
		.header {
			padding: 10px 1rem;
		}

		.mainNav {
			display: flex;
			position: fixed;
			top: 0;
			left: 0;
			width: 100vw;
			height: 100vh;
			background: white !important;
			transform: translateX(100%);
			transition: transform 0.3s ease-in-out;
			z-index: 100;
			padding: 0;
			margin: 0;
		}

		.nav-links {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			width: 100%;
			height: 100%;
			gap: 2rem;
		}

		.logo {
			font-size: 1.5rem;
		}

		.mainNav.open {
			transform: translateX(0);
		}

		.mainNav a {
			font-size: 1.5rem;
		}

		.menu-toggle {
			padding: none;
		}

		button {
			padding: none;
		}
	}
</style>
