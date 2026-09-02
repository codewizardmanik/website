<svelte:head>
	<title>misc</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" />
	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main
	class="min-h-screen bg-[#080808] text-white flex flex-col items-center justify-center text-center p-8 selection:bg-[#16e16e] selection:text-black font-['Funnel_Display']"
>
	<h1 class="text-5xl font-['Instrument_Serif'] text-[#16e16e] mb-6">
		nothing here <span class="text-[#ff69b4]">(yet)</span>
	</h1>

	<div class="max-w-xl mx-auto space-y-4 px-4 text-sm md:text-base text-gray-300">
		<a href="/" class="inline-block mt-2 italic hover:underline text-[#16e16e] transition-colors"
			>go back home</a
		>
	</div>

	<div class="flex flex-wrap justify-center gap-6 text-sm mt-8 font-['Funnel_Display']">
		<a class="text-[#16e16e] transition-colors" href="/">/</a>
		<a class="text-[#16e16e] transition-colors" href="/about">/about</a>
		<a class="text-[#16e16e] transition-colors" href="/blog">/blog</a>
		<a class="text-[#16e16e] transition-colors" href="/projects">/projects</a>
		<a class="text-[#16e16e] transition-colors" href="/webrings">sillies</a>
		<a class="transition-colors font-bold text-[#16e16e]" href="/misc">/misc</a>
	</div>
</main>
