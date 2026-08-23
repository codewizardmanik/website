<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { fly } from 'svelte/transition';

	const quotes = [
		'manik',
		'a goofy guy',
		'a student',
		'a.. what?',
		'a developer',
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
</svelte:head>

<main class="min-h-screen flex flex-col items-center justify-center text-center p-4 text-white">
	<h2 class="text-xl font-[Instrument_Serif]">hi, im</h2>
	<span class="block mb-1 h-8 overflow-hidden">
		{#key quote}
			<h2
				class="block text-2xl font-[Instrument_Serif] text-[#81E979]"
				transition:fly={{ x: 10, duration: 300 }}
			>
				{quote}
			</h2>
		{/key}
	</span>

	<div class="mx-auto text-left">
		<p>i do a lot of random stuff. im (currently) a 14 year old student.</p>
		<p class="text-[10px] font-[Jetbrains_Mono]">
			im part of my schools tech club (well 2 of them), <a
				class="link"
				href="https://robonexus46.vercel.app/">robonexus</a
			>
			and
			<a class="link" href="https://techsyndicate.us">tech syndicate</a>
		</p>
	</div>

	<!-- deez are website links -->
	<div class="mt-6 flex gap-4 font-[Jetbrains_Mono]">
		<a class="font-bold link" href="/">/</a>
		<a class="link" href="/about">/about</a>
		<a class="link" href="/blog">/blog</a>
		<a class="link" href="/projects">/projects</a>
		<a class="link" href="/webrings">sillies</a>
		<a class="link" href="/misc">/misc</a>
	</div>

	<!-- deez are other links -->
	<div class="mt-6 flex gap-4 font-[Jetbrains_Mono]">
		<a class="link" href="https://github.com/codewizardmanik">github</a>
		<a class="link" href="https://www.youtube.com/@codewizardmanik">yt</a>
		<a class="link" href="https://www.instagram.com/m4n1k.sh/">ig</a>
		<a class="link" href="mailto:m4.sh@tuta.io"> email </a>
		<a class="link" href="https://www.linkedin.com/in/manik-sharma-30b4a9419/">linkedin</a>
		<a class="link" href="https://vncl.xyz">""company"" website</a>
	</div>
	<p class="text-xs font-[Jetbrains_Mono]">
		my links are also available @ <a class="link" href="https://links.maniksharma.xyz"
			>https://links.maniksharma.xyz</a
		>
	</p>
	<br />
	<p class="text-[9px] font-[Jetbrains_Mono]">
		<span class="italic">psst</span> want to listen to a banger song?
		<a href="https://www.youtube.com/watch?v=3eD4CrAmwNk" target="_blank" class="link"
			>click here (creep x call me maybe)</a
		>
		or
		<a
			href="https://open.spotify.com/track/5rUFgYSgfDajlankhu3Kld?si=e2105c0d36904c19"
			target="_blank"
			class="link"
		>
			here (all mine)</a
		>
		or
		<a
			href="https://open.spotify.com/track/6b37xrsNCWYIUphFBazqD6?si=b346bd012bea4270"
			target="_blank"
			class="link">here (me gustas tu)</a
		>
	</p>
</main>
