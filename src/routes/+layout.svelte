<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.ico';
	import logo from '$lib/assets/attensi-logo.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@400;600;700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<header class="border-b-3 border-accent bg-text text-white">
	<div class="mx-auto flex max-w-280 items-center gap-4 p-5 sm:gap-6">
		<img src={logo} alt="Attensi" class="block w-32.5 sm:w-43.5" />
		<span class="text-md border-l border-subtle-border pl-4 font-semibold sm:pl-6"
			>Tinne Jacobs</span
		>
	</div>
</header>

{@render children()}
