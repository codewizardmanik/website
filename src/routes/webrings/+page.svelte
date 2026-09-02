<script lang="ts">
	import { onMount } from 'svelte';
	import { browser } from '$app/environment';

	onMount(() => {
		if (!browser) return;

		function loadScript(src: string, attrs = {}) {
			if (document.querySelector(`script[src="${src}"]`)) return null;
			const s = document.createElement('script');
			s.src = src;
			for (const [k, v] of Object.entries(attrs)) s.setAttribute(k, v);
			document.body.appendChild(s);
			return s;
		}

		const scripts = [
			loadScript(
				'https://darkosparko.nekoweb.org/webrings/apartments-webring/apartment-webring-variables.js'
			),
			loadScript(
				'https://darkosparko.nekoweb.org/webrings/apartments-webring/apartment-webring-widget.js'
			),
			loadScript('https://silly.possiblyaxolotl.com/ring/webstring.js'),
			loadScript(
				'https://jack-dawlia.neocities.org/page/shrines/portal/aperturewebring/onionring-variables.js'
			),
			loadScript(
				'https://jack-dawlia.neocities.org/page/shrines/portal/aperturewebring/onionring-widget-1.js'
			),
			loadScript('https://tfortring.neocities.org/fortring/onionring-variables.js'),
			loadScript('https://tfortring.neocities.org/fortring/onionring-widget.js'),
			loadScript('https://fabstarotcorner.neocities.org/webring/onionring-variables.js'),
			loadScript('https://fabstarotcorner.neocities.org/webring/onionring-widget.js'),
			loadScript('https://homebrew.cresentri.com/webring.js'),
			loadScript('https://mechagic.pages.gay/1stylescripts/webring/gitgudring.js', {
				defer: 'defer'
			})
		];

		return () => scripts.forEach((s) => s?.remove());
	});
</script>

<svelte:head>
	<title>sillies</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
	<link
		rel="stylesheet"
		href="https://jack-dawlia.neocities.org/page/shrines/portal/aperturewebring/onionring.css"
	/>
	<link rel="stylesheet" href="https://tfortring.neocities.org/fortring/onionring.css" />
	<link
		rel="stylesheet"
		href="https://darkosparko.nekoweb.org/webrings/apartments-webring/apartment-webring-style.css"
	/>
</svelte:head>

<main
	class="min-h-screen bg-[#080808] text-white flex flex-col items-center justify-between p-8 selection:bg-[#16e16e] selection:text-black font-['Funnel_Display']"
>
	<div class="flex flex-col items-center w-full max-w-xl mx-auto py-8">
		<h2 class="text-5xl font-['Instrument_Serif'] text-[#16e16e] mb-1">sillies!</h2>
		<p class="text-xs text-[#ff69b4] italic mb-4">(warning: kinda broken)</p>
		<div class="flex flex-wrap justify-center gap-6 text-sm font-['Funnel_Display']">
			<a class="text-[#16e16e] transition-colors" href="/">/</a>
			<a class="text-[#16e16e] transition-colors" href="/about">/about</a>
			<a class="text-[#16e16e] transition-colors" href="/blog">/blog</a>
			<a class="text-[#16e16e] transition-colors" href="/projects">/projects</a>
			<a class="transition-colors font-bold text-[#16e16e]" href="/webrings">sillies</a>
			<a class="text-[#16e16e] transition-colors" href="/misc">/misc</a>
		</div>

		<hr class="w-[80%] my-4 opacity-20 border-[#16e16e]" />

		<div class="flex flex-col items-center gap-4 w-full">
			<img src="bestvieweddesktop.gif" alt="THIS WEBSITE IS BEST VIEWED ON DESKTOP" />
			<a href="https://archive.org" target="_blank" rel="noreferrer"
				><img src="internet archive.gif" alt="Internet Archive." /></a
			>
			<a href="https://face.dev" target="_blank" rel="noreferrer"
				><img src="matrix.png" alt="Wake up, Neo..." /></a
			>
			<a href="https://notbyai.fyi/" target="_blank" rel="noreferrer"
				><img src="Scripted-By-a-Human-Not-By-AI-Badge-black.png" alt="Scripted by a human" /></a
			>
			<a href="https://people.pledge.party" target="_blank" rel="noreferrer">
				<img src="people_pledge_badge_seal_black_white_100x100.png" alt="Pledge Party" />
			</a>
			<a href="https://www.mabsland.com/Adoption.html" target="_blank" rel="noreferrer">
				<img
					src="Censor_14c.gif"
					alt="This site contains slightly offensive material. High chance of mild swearing, partial nudity, violence and adult themes."
				/>
			</a>
			<a
				href="https://nonbot.org/pledged/view/a09d990e-c888-4639-83b9-04c0e69ba5b9"
				target="_blank"
				rel="noreferrer"
			>
				<img
					style="height:128px;margin-top:10px;margin-bottom:10px;"
					src="https://nonbot.org/images/nonbot_pledged_logo.svg"
					alt="Human-made Content"
				/>
			</a>
			<a href="https://evehibi.nekoweb.org/ringlink/info.html" target="_blank" rel="noreferrer">
				<img
					src="https://evehibi.nekoweb.org/ringlink/button.gif"
					alt="ringlink - advertise your webring!"
				/>
			</a>
			<a href="https://team.indieseas.net" target="_blank" rel="noreferrer"
				><img
					src="https://team.indieseas.net/img/indiefellas.svg"
					alt="indiefellas"
					class="button"
				/></a
			>

			<iframe
				src="//incr.easrng.net/badge?key=maniksharma"
				style="background: url(//incr.easrng.net/bg.gif)"
				title="increment badge"
				width="88"
				height="31"
				frameborder="0"
			></iframe>

			<div class="flex items-center gap-3 text-sm">
				<a
					class="text-[#16e16e] hover:underline transition-colors px-2"
					href="https://webring.dinhe.net/prev/https://maniksharma.xyz">prev</a
				>
				<a
					class="text-gray-300 hover:text-[#16e16e] transition-colors"
					href="https://webring.dinhe.net">retronaut-webring</a
				>
				<a
					class="text-[#16e16e] hover:underline transition-colors px-2"
					href="https://webring.dinhe.net/next/https://maniksharma.xyz">next</a
				>
			</div>

			<div class="flex items-center gap-3 text-sm">
				<a
					class="text-[#16e16e] hover:underline transition-colors px-2"
					href="https://hotlinewebring.club/beigestack/previous">prev</a
				>
				<a
					class="text-gray-300 hover:text-[#16e16e] transition-colors"
					href="https://hotlinewebring.club">hotline-webring</a
				>
				<a
					class="text-[#16e16e] hover:underline transition-colors px-2"
					href="https://hotlinewebring.club/beigestack/next">next</a
				>
			</div>

			<a href="http://internetometer.com/give/51711" target="_blank" rel="noreferrer"
				><img src="http://internetometer.com/image/51711.png" alt="internetometer" /></a
			>

			<div class="flex gap-4">
				<img src="copilot.png" alt="COPILOT WILL DOOM US ALLLL" />
				<img src="windowscola.gif" alt="its a.. windows cola?" />
			</div>

			<iframe
				src="https://codewizardmanik.github.io/website-old/webring-widget.html?site=https://maniksharma.xyz"
				width="360"
				height="140"
				frameborder="0"
				scrolling="no"
				style="border:none; overflow:hidden;"
				title="old webring widget"
			></iframe>

			<div id="apartment-webring"></div>
			<div id="aperturewebring">
				<noscript>
					This site is part of the <a
						href="https://jack-dawlia.neocities.org/page/shrines/portal/aperturewebring"
						class="text-[#16e16e] hover:underline">Aperture Webring</a
					>!
				</noscript>
			</div>

			<map name="w95widget">
				<area
					href="https://baccyflap.com/noai"
					target="_blank"
					shape="rect"
					coords="0,0,308,22"
					alt="no ai webring"
					title="no ai webring"
				/>
				<area
					href="https://baccyflap.com/noai/?prv&s=dll"
					target="_top"
					shape="rect"
					coords="56,36,130,58"
					alt="previous"
					title="previous"
				/>
				<area
					href="https://baccyflap.com/noai/?rnd"
					target="_top"
					shape="rect"
					coords="137,36,211,58"
					alt="random"
					title="random"
				/>
				<area
					href="https://baccyflap.com/noai/?nxt&s=dll"
					target="_top"
					shape="rect"
					coords="218,36,292,58"
					alt="next"
					title="next"
				/>
			</map>
			<img
				usemap="#w95widget"
				src="https://baccyflap.com/noai/w95widget.gif"
				alt="a gray Windows 95 style dialog box titled 'The No AI Webring'"
			/>

			<div id="fortring"></div>
			<div id="gfdkris"></div>

			<map name="badge-wwstamp">
				<area
					shape="rect"
					coords="66,38,79,49"
					href="https://webmasterwebring.netlify.app?beigestack-previous"
					alt="Previous"
				/>
				<area
					shape="rect"
					coords="78,29,90,40"
					href="https://webmasterwebring.netlify.app?beigestack-next"
					alt="Next"
				/>
				<area
					shape="rect"
					coords="13,15,63,47"
					href="https://webmasterwebring.netlify.app"
					alt="Webmaster Webring"
				/>
			</map>
			<img
				usemap="#badge-wwstamp"
				id="ww-stamp"
				src="https://file.garden/ZrZSgsrYfQXsO7QH/ww/stamp.png"
				alt="Webmaster Webring"
				width="99"
				height="56"
			/>
		</div>

		<hr class="w-[80%] my-6 opacity-20 border-[#16e16e]" />
	</div>
</main>
