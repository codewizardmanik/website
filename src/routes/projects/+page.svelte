<svelte:head>
	<title>projects</title>
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
		hi gng <span class="text-[#ff69b4]">(projects)</span>
	</h2>

	<div class="max-w-xl mx-auto space-y-3 px-4 text-sm md:text-base text-gray-300 text-left">
		<p>
			> this website lmao (svelte + tailwind) <a
				href="https://github.com/sudofahh"
				class="text-[#16e16e] hover:underline transition-colors ml-1"
				target="_blank">github here</a
			>
		</p>
		<p>
			> vnOS (os stuff like C and ASM etc.) <a
				href="https://github.com/sudofahh/vnOS"
				class="text-[#16e16e] hover:underline transition-colors ml-1"
				target="_blank">github here</a
			>
		</p>
		<p>> quicksave, cairn, kontentklear, tenquestions, cozycup etc. (svelte + tailwind)</p>
		<p>
			> nimbleGTK (GTKJS) <a
				href="https://github.com/sudofahh/NimbleGTK"
				class="text-[#16e16e] hover:underline transition-colors ml-1"
				target="_blank">github here</a
			>
		</p>
		<p>
			> fahh (linux command and macos command that plays fahh.mp4 haha) <a
				href="https://github.com/sudofahh/fahh"
				class="text-[#16e16e] hover:underline transition-colors ml-1"
				target="_blank">github here</a
			>
		</p>
		<p>> techsyndicate and robonexus (school)</p>
	</div>

	<div class="flex flex-wrap justify-center gap-6 text-sm mt-8 font-['Funnel_Display']">
		<a class="text-[#16e16e] transition-colors" href="/">/</a>
		<a class="text-[#16e16e] transition-colors" href="/about">/about</a>
		<a class="text-[#16e16e] transition-colors" href="/blog">/blog</a>
		<a class="transition-colors font-bold text-[#16e16e]" href="/projects">/projects</a>
		<a class="text-[#16e16e] transition-colors" href="/webrings">sillies</a>
		<a class="text-[#16e16e] transition-colors" href="/misc">/misc</a>
	</div>
</main>
