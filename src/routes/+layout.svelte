<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import inactiveFavicon from '$lib/assets/inactive.svg';

	let { children } = $props();

	let timeout: ReturnType<typeof setTimeout>;

	function updateFavicon() {
		clearTimeout(timeout);

		if (document.visibilityState === 'visible') {
			document.querySelector<HTMLLinkElement>('link[rel="icon"]')!.href = favicon;
		} else {
			timeout = setTimeout(() => {
				if (document.visibilityState === 'hidden') {
					document.querySelector<HTMLLinkElement>('link[rel="icon"]')!.href =
						inactiveFavicon;
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
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="relative min-h-screen w-full bg-[#363635] overflow-hidden">
	<div class="absolute inset-0 flex items-center justify-center opacity-25 pointer-events-none">
		<video autoplay loop muted playsinline preload="auto" class="w-[45%] h-auto">
			<source src="/pyramid.webm" type="video/webm" />
			<source src="/pyramid.mp4" type="video/mp4" />
		</video>
	</div>

	<div class="relative z-10 w-full min-h-screen">
		{@render children()}
	</div>
</div>
