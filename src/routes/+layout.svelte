<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import inactiveFavicon from '$lib/assets/inactive.svg';
	import { onMount } from 'svelte';
	import { page } from '$app/state';

	let { children } = $props();

	// Favicon visibility state
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

	// Global Marquee state & Navigation tracking
	const marqueeText = 'MANIK SHARMA • MANIK SHARMA ✦ MANIK SHARMA • '.repeat(16);

	let leftOffset = $state(0);
	let rightOffset = $state(0);
	let isResetting = $state(false);
	let isPaused = $state(false);

	let lastPath = page.url.pathname;
	let isMounted = false;
	let resetTimeout: ReturnType<typeof setTimeout>;

	// Detect page navigation changes
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
				// Move backward quickly until it reaches 0 (the start)
				leftOffset += 5;
				rightOffset += 5;

				if (leftOffset >= 0 && rightOffset >= 0) {
					leftOffset = 0;
					rightOffset = 0;

					isResetting = false;
					isPaused = true;

					// Delay before starting scrolling again
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
	class="h-screen w-screen overflow-hidden bg-black text-white relative selection:bg-[#16e16e] selection:text-black font-['Funnel_Display']"
>
	<!-- LEFT MARQUEE -->
	<aside
		class="fixed top-0 bottom-0 left-4 md:left-6 w-10 md:w-12 bg-black z-50 border-x border-white/30 overflow-hidden pointer-events-none select-none flex flex-col items-center"
	>
		<div
			class="absolute flex flex-col items-center whitespace-nowrap will-change-transform"
			style="transform: translateY({leftOffset}px);"
		>
			<div
				class="flex flex-col items-center text-lg md:text-xl font-bold tracking-widest text-white py-2 [writing-mode:vertical-rl]"
			>
				{marqueeText}
			</div>

			<div
				class="flex flex-col items-center text-lg md:text-xl font-bold tracking-widest text-white py-2 [writing-mode:vertical-rl]"
				aria-hidden="true"
			>
				{marqueeText}
			</div>
		</div>
	</aside>

	<!-- RIGHT MARQUEE - FACING INWARD -->
	<aside
		class="fixed top-0 bottom-0 right-4 md:right-6 w-10 md:w-12 bg-black z-50 border-x border-white/30 overflow-hidden pointer-events-none select-none flex flex-col items-center"
	>
		<div
			class="absolute flex flex-col items-center whitespace-nowrap will-change-transform"
			style="transform: translateY({rightOffset}px);"
		>
			<!-- Same writing mode as left, but flipped 180° -->
			<div
				class="flex flex-col items-center text-lg md:text-xl font-bold tracking-widest text-white py-2 [writing-mode:vertical-rl] rotate-180"
			>
				{marqueeText}
			</div>

			<div
				class="flex flex-col items-center text-lg md:text-xl font-bold tracking-widest text-white py-2 [writing-mode:vertical-rl] rotate-180"
				aria-hidden="true"
			>
				{marqueeText}
			</div>
		</div>
	</aside>

	<!-- PAGE CONTENT WRAPPER -->
	<div class="relative z-10 w-full h-full px-16 md:px-28">
		{@render children()}
	</div>
</div>
