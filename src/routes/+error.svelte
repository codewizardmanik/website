<script lang="ts">
	import { page } from '$app/state';
</script>

<svelte:head>
	<title>{page.status === 404 ? '404 - page not found' : `${page.status} - error`}</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main
	class="min-h-screen bg-[#080808] text-white flex flex-col items-center justify-between p-8 selection:bg-[#16e16e] selection:text-black font-['Funnel_Display']"
>
	<div
		class="flex flex-col items-center justify-center my-auto w-full max-w-xl mx-auto px-4 text-center"
	>
		{#if page.status === 404}
			<h1 class="text-5xl font-['Instrument_Serif'] text-[#16e16e] mb-4">404 (page not found)</h1>
			<a href="/" class="text-[#16e16e] hover:underline transition-colors mt-2 inline-block"
				>go back home</a
			>
			<p class="text-xs font-mono text-gray-400 mt-6">
				if you think this is a mistake, please <a
					href="mailto:m4.sh@tuta.io"
					class="text-[#16e16e] hover:underline transition-colors">contact me</a
				>
			</p>
		{:else}
			<h1 class="text-5xl font-['Instrument_Serif'] text-[#16e16e] mb-4">
				{page.status}: {page.error?.message}
			</h1>
			<a href="/" class="text-[#16e16e] hover:underline transition-colors mt-2 inline-block"
				>go back home</a
			>
			<p class="text-xs text-gray-400 mt-6">
				if you think this is a mistake, please <a
					href="mailto:m4.sh@tuta.io"
					class="text-[#16e16e] hover:underline transition-colors">contact me</a
				>
			</p>
		{/if}
	</div>
</main>
