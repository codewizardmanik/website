<svelte:head>
	<title>blog</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main
	class="min-h-screen bg-[#080808] text-white flex flex-col items-center justify-center text-center p-8 selection:bg-[#16e16e] selection:text-black font-['Funnel_Display']"
>
	<h2 class="text-5xl font-['Instrument_Serif'] text-[#16e16e] mb-6">hi gng (blog)</h2>

	<div class="max-w-xl mx-auto space-y-4 px-4 text-sm md:text-base text-gray-300">
		<div class="flex flex-col gap-3">
			<a
				href="/posts/why-ai-is-good-but-bad.txt"
				class="text-[#16e16e] hover:underline transition-colors">first post</a
			>
			<a
				href="/posts/me-yapping-about-vehicles.txt"
				class="text-[#16e16e] hover:underline transition-colors">second post</a
			>
			<a
				href="/posts/poem-about-a-stray.txt"
				class="text-[#16e16e] hover:underline transition-colors">third post</a
			>
			<a href="/posts/story6.txt" class="text-[#16e16e] hover:underline transition-colors"
				>fourth post</a
			>
			<a href="/posts/nobodytalks.txt" class="text-[#16e16e] hover:underline transition-colors"
				>fifth post</a
			>
		</div>
		<p class="text-xs text-gray-400 pt-2">btw these may/may not remain .txt files</p>
	</div>

	<div class="flex flex-wrap justify-center gap-6 text-sm mt-8 font-['Funnel_Display']">
		<a class="text-[#16e16e] transition-colors" href="/">/</a>
		<a class="text-[#16e16e] transition-colors" href="/about">/about</a>
		<a class="transition-colors font-bold text-[#16e16e]" href="/blog">/blog</a>
		<a class="text-[#16e16e] transition-colors" href="/projects">/projects</a>
		<a class="text-[#16e16e] transition-colors" href="/webrings">sillies</a>
		<a class="text-[#16e16e] transition-colors" href="/misc">/misc</a>
	</div>
</main>
