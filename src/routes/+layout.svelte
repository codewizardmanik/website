<script lang="ts">
	import './layout.css';
	import Cursor from '$lib/Cursor.svelte';
	import favicon from '$lib/assets/favicon.svg';
	import inactiveFavicon from '$lib/assets/inactive.svg';
	import { onMount } from 'svelte';
	import { page } from '$app/state';

	let { children } = $props();

	let timeout: ReturnType<typeof setTimeout>;

	function updateFavicon() {
		clearTimeout(timeout);

		if (document.visibilityState === 'visible') {
			document.querySelector<HTMLLinkElement>('link[rel="icon"]')!.href = favicon;
		} else {
			timeout = setTimeout(() => {
				if (document.visibilityState === 'hidden') {
					document.querySelector<HTMLLinkElement>('link[rel="icon"]')!.href = inactiveFavicon;
				}
			}, 500);
		}
	}

	$effect(() => {
		updateFavicon();
		document.addEventListener('visibilitychange', updateFavicon);

		return () => {
			clearTimeout(timeout);
			document.removeEventListener('visibilitychange', updateFavicon);
		};
	});

	const marqueeText = 'MANIK SHARMA • MANIK SHARMA ✦ MANIK SHARMA • '.repeat(16);

	let leftOffset = $state(0);
	let rightOffset = $state(0);
	let isResetting = $state(false);
	let isPaused = $state(false);

	let lastPath = page.url.pathname;
	let isMounted = false;
	let resetTimeout: ReturnType<typeof setTimeout>;

	$effect(() => {
		const currentPath = page.url.pathname;

		if (isMounted && currentPath !== lastPath) {
			lastPath = currentPath;

			clearTimeout(resetTimeout);

			isPaused = false;
			isResetting = true;
		}
	});

	onMount(() => {
		isMounted = true;

		let animationFrameId: number;

		function updateMarquee() {
			if (isResetting) {
				leftOffset += 6;
				rightOffset += 6;

				if (leftOffset >= 0 && rightOffset >= 0) {
					leftOffset = 0;
					rightOffset = 0;

					isResetting = false;
					isPaused = true;

					resetTimeout = setTimeout(() => {
						isPaused = false;
					}, 250);
				}
			} else if (!isPaused) {
				leftOffset -= 0.6;
				rightOffset -= 0.6;
			}

			animationFrameId = requestAnimationFrame(updateMarquee);
		}

		animationFrameId = requestAnimationFrame(updateMarquee);

		return () => {
			cancelAnimationFrame(animationFrameId);
			clearTimeout(resetTimeout);
		};
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />

	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />

	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div
	class="relative h-screen w-screen overflow-hidden bg-black font-['Funnel_Display'] text-white selection:bg-[#16e16e] selection:text-black"
>
	<!-- LEFT MARQUEE -->
	<aside
		class="pointer-events-none fixed bottom-0 left-6 top-0 z-50 hidden w-12 flex-col items-center overflow-hidden border-x border-white/30 bg-black select-none md:flex"
	>
		<div
			class="absolute flex flex-col items-center whitespace-nowrap will-change-transform"
			style="transform: translateY({leftOffset}px);"
		>
			{#each Array(4) as _, i}
				<div
					class="flex flex-col items-center py-2 text-lg font-bold tracking-widest text-white md:text-xl [writing-mode:vertical-rl]"
					class:pointer-events-auto={i === 0}
					aria-hidden={i !== 0}
					data-cursor={i === 0 ? 'hehe my website yes yes how grand' : undefined}
				>
					{marqueeText}
				</div>
			{/each}
		</div>
	</aside>

	<!-- RIGHT MARQUEE - FACING INWARD -->
	<aside
		class="pointer-events-none fixed bottom-0 right-6 top-0 z-50 hidden w-12 flex-col items-center overflow-hidden border-x border-white/30 bg-black select-none md:flex"
	>
		<div
			class="absolute flex flex-col items-center whitespace-nowrap will-change-transform"
			style="transform: translateY({rightOffset}px);"
		>
			{#each Array(4) as _, i}
				<div
					class="flex flex-col items-center py-2 text-lg font-bold tracking-widest text-white md:text-xl [writing-mode:vertical-rl] rotate-180"
					class:pointer-events-auto={i === 0}
					aria-hidden={i !== 0}
					data-cursor={i === 0 ? 'here too' : undefined}
				>
					{marqueeText}
				</div>
			{/each}
		</div>
	</aside>

	<Cursor />

	<!-- PAGE CONTENT WRAPPER -->
	<div class="relative z-10 h-full w-full px-6 md:px-28">
		{@render children()}
	</div>
</div>
