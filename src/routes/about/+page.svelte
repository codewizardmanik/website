<svelte:head>
	<title>about meh</title>
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
	<h2 class="text-5xl font-['Instrument_Serif'] text-[#16e16e] mb-6">
		hi gng <span class="text-[#ff69b4]">(whoami)</span>
	</h2>

	<div class="max-w-xl mx-auto space-y-4 px-4 text-sm md:text-base text-gray-300">
		<p>
			My name is Manik Sharma. I'm 14 (in 2026). I like to code, do cryptics, do random stuff with
			arduinos and such, read books (including <a
				href="https://omniscient-readers-viewpoint.fandom.com/wiki/Omniscient_Reader%27s_Viewpoint"
				class="text-[#16e16e] italic hover:underline font-mono"
				target="_blank">orv</a
			>, I highly recommend it), listen to music, use fedora linux and so on and so forth bla bla
			bla (i have wayy too many interests for my own good 😭 help me)
		</p>
		<div class="text-left text-xs text-gray-400">
			<p class="font-mono text-[#16e16e]/80">abh aur kya janna h, bhaag jao</p>
		</div>
	</div>

	<div class="flex flex-wrap justify-center gap-6 text-sm mt-8 font-['Funnel_Display']">
		<a class="text-[#16e16e] transition-colors" href="/">/</a>
		<a class="transition-colors font-bold text-[#16e16e]" href="/about">/about</a>
		<a class="text-[#16e16e] transition-colors" href="/blog">/blog</a>
		<a class="text-[#16e16e] transition-colors" href="/projects">/projects</a>
		<a class="text-[#16e16e] transition-colors" href="/webrings">sillies</a>
		<a class="text-[#16e16e] transition-colors" href="/misc">/misc</a>
	</div>
</main>
