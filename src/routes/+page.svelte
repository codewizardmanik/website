<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { fly } from 'svelte/transition';

	const quotes = [
		'a developer',
		'a goofy guy',
		'a student',
		'a.. what?',
		'a neeeeeeeeeeeerd',
		'an exception(e)',
		'a python coder (spare me)'
	];

	let quote = $state(quotes[0]);
	let lastIndex = -1;
	let interval: ReturnType<typeof setInterval>;

	onMount(() => {
		interval = setInterval(() => {
			let index;
			do {
				index = Math.floor(Math.random() * quotes.length);
			} while (index === lastIndex);

			lastIndex = index;
			quote = quotes[index];
		}, 4000);
	});

	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<svelte:head>
	<title>this is the website of {quote}</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main
	class="h-screen overflow-y-scroll snap-y snap-mandatory bg-black text-white selection:bg-[#16e16e] selection:text-black scroll-smooth"
>
	<div
		class="h-screen w-full snap-start flex flex-col items-center justify-center relative shrink-0 p-4"
	>
		<div
			class="w-[500px] h-[540px] relative flex flex-col justify-between p-6 border bg-black border-0"
		>
			<div class="font-['Funnel_Display'] text-xl text-white select-none">hi, i'm</div>

			<div class="flex flex-col items-center justify-center relative my-auto">
				<span
					class="absolute left-2 top-1/2 -translate-y-1/2 text-[#ff69b4] text-3xl select-none inline-block animate-cute-rotate"
					>✦</span
				>

				<h1
					class="font-['Instrument_Serif'] text-[#16e16e] text-[9.5rem] leading-none tracking-tight text-center w-full select-none"
				>
					manik
				</h1>

				<span
					class="absolute right-2 top-1/2 -translate-y-1/2 text-[#ff69b4] text-3xl select-none inline-block animate-cute-rotate-reverse"
					>✦</span
				>
			</div>

			<div
				class="flex items-center justify-center gap-2 font-['Funnel_Display'] text-xl text-white select-none pb-2"
			>
				<span>i'm</span>
				<span class="h-10 w-72 relative overflow-hidden inline-block">
					{#key quote}
						<span
							class="font-['Instrument_Serif'] text-[#16e16e] text-3xl absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 inline-block whitespace-nowrap text-center w-full"
							transition:fly={{ y: 15, duration: 300 }}
						>
							{quote}
						</span>
					{/key}
				</span>
			</div>
		</div>

		<div
			class="absolute bottom-6 left-1/2 -translate-x-1/2 animate-bounce text-xs font-['Funnel_Display'] tracking-widest text-[#16e16e] opacity-80 select-none"
		>
			scroll down ↓
		</div>
	</div>

	<section
		class="h-screen w-full snap-start flex flex-col items-center justify-center text-center py-16 gap-6 font-['Funnel_Display'] shrink-0 overflow-y-auto px-4"
	>
		<div class="max-w-xl mx-auto space-y-3 px-4 text-sm md:text-base text-gray-300">
			<p>i do a lot of random stuff. im (currently) a 14 year old student.</p>
			<p class="text-xs text-gray-400">
				im part of my schools tech club (well 2 of them),
				<a
					class="text-[#16e16e] hover:underline"
					href="https://robonexus46.vercel.app/"
					target="_blank">robonexus</a
				>
				and
				<a class="text-[#16e16e] hover:underline" href="https://techsyndicate.us" target="_blank"
					>tech syndicate</a
				>
			</p>
		</div>

		<div class="flex flex-wrap justify-center gap-6 text-sm">
			<a class="text-[#16e16e] transition-colors font-bold" href="/">/</a>
			<a class="text-[#16e16e] transition-colors hover:underline" href="/about">/about</a>
			<a class="text-[#16e16e] transition-colors hover:underline" href="/blog">/blog</a>
			<a class="text-[#16e16e] transition-colors hover:underline" href="/projects">/projects</a>
			<a class="text-[#16e16e] transition-colors hover:underline" href="/webrings">sillies</a>
			<a class="text-[#16e16e] transition-colors hover:underline" href="/misc">/misc</a>
		</div>

		<div class="flex flex-wrap justify-center gap-6 text-sm text-gray-400">
			<a
				class="transition-colors hover:underline"
				href="https://github.com/codewizardmanik"
				target="_blank">github</a
			>
			<a
				class="transition-colors hover:underline"
				href="https://www.youtube.com/@codewizardmanik"
				target="_blank">yt</a
			>
			<a
				class="transition-colors hover:underline"
				href="https://www.instagram.com/m4n1k.sh/"
				target="_blank">ig</a
			>
			<a class="transition-colors hover:underline" href="mailto:m4.sh@tuta.io">email</a>
			<a
				class="transition-colors hover:underline"
				href="https://www.linkedin.com/in/manik-sharma-30b4a9419/"
				target="_blank">linkedin</a
			>
			<a class="transition-colors hover:underline" href="https://vncl.xyz" target="_blank"
				>""company"" website</a
			>
		</div>

		<p class="text-xs text-gray-500">
			my links are also available @ <a
				class="text-[#16e16e] hover:underline"
				href="https://links.maniksharma.xyz"
				target="_blank">https://links.maniksharma.xyz</a
			>
		</p>

		<div class="text-[11px] text-gray-400 mt-2 max-w-md">
			<span class="italic">psst</span> want to listen to a banger song?<br />
			<a
				href="https://www.youtube.com/watch?v=3eD4CrAmwNk"
				target="_blank"
				class="text-[#16e16e] hover:underline">click here (creep x call me maybe)</a
			>
			or
			<a
				href="https://open.spotify.com/track/5rUFgYSgfDajlankhu3Kld?si=e2105c0d36904c19"
				target="_blank"
				class="text-[#16e16e] hover:underline">here (all mine)</a
			>
			or
			<a
				href="https://open.spotify.com/track/6b37xrsNCWYIUphFBazqD6?si=b346bd012bea4270"
				target="_blank"
				class="text-[#16e16e] hover:underline">here (me gustas tu)</a
			>
		</div>
	</section>
</main>

<style>
	@keyframes cuteRotate {
		0% {
			transform: rotate(0deg);
		}
		25% {
			transform: rotate(45deg);
		}
		50% {
			transform: rotate(-45deg);
		}
		100% {
			transform: rotate(0deg);
		}
	}

	@keyframes cuteRotateReverse {
		0% {
			transform: rotate(0deg);
		}
		25% {
			transform: rotate(45deg);
		}
		50% {
			transform: rotate(-45deg);
		}
		100% {
			transform: rotate(0deg);
		}
	}

	.animate-cute-rotate {
		animation: cuteRotate 4s ease-in-out infinite;
	}

	.animate-cute-rotate-reverse {
		animation: cuteRotateReverse 4s ease-in-out infinite;
	}
</style>
