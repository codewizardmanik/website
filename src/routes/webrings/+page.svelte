<script>
	import { onMount } from 'svelte';
	import { browser } from '$app/environment';

	function setHoverGifText(e) {
		e.target.src = 'https://maniksharma.xyz/hover-text.gif?t=' + Date.now();
	}
	function setIdleGifText(e) {
		e.target.src = 'https://maniksharma.xyz/idle.gif';
	}
	function setHoverGif(e) {
		e.target.src = 'https://maniksharma.xyz/hover.gif?t=' + Date.now();
	}
	function setIdleGif(e) {
		e.target.src = 'https://maniksharma.xyz/idle.gif';
	}

	onMount(() => {
		if (!browser) return;

		function loadScript(src, attrs = {}) {
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

		return () => scripts.forEach((s) => s.remove());
	});
</script>

<svelte:head>
	<title>webrings</title>
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

<main class="min-h-screen flex flex-col items-center text-center p-4 text-white">
	<h2 class="text-2xl font-[Instrument_Serif] text-[#81E979] mt-4">sillies!</h2>

	<hr class="w-[80%] my-4 opacity-30" />

	<div class="flex flex-col items-center gap-3">
		<img src="bestvieweddesktop.gif" alt="THIS WEBSITE IS BEST VIEWED ON DESKTOP" />
		<a href="https://archive.org"><img src="internet archive.gif" alt="Internet Archive." /></a>
		<a href="https://face.dev"><img src="matrix.png" alt="Wake up, Neo..." /></a>
		<a href="https://notbyai.fyi/"
			><img src="Scripted-By-a-Human-Not-By-AI-Badge-black.png" alt="Scripted by a human" /></a
		>
		<a href="https://people.pledge.party">
			<img src="people_pledge_badge_seal_black_white_100x100.png" alt="Pledge Party" />
		</a>
		<a href="https://www.mabsland.com/Adoption.html">
			<img
				src="Censor_Gc.gif"
				alt="This website is rated G. There is no explicit content on this page."
			/>
		</a>
		<a href="https://nonbot.org/pledged/view/a09d990e-c888-4639-83b9-04c0e69ba5b9" target="_blank">
			<img
				style="height:128px;margin-top:10px;margin-bottom:10px;"
				src="https://nonbot.org/images/nonbot_pledged_logo.svg"
				alt="Human-made Content"
			/>
		</a>
		<a href="https://evehibi.nekoweb.org/ringlink/info.html" target="_blank">
			<img
				src="https://evehibi.nekoweb.org/ringlink/button.gif"
				alt="ringlink - advertise your webring!"
			/>
		</a>
		<a href="https://team.indieseas.net"
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

		<div class="flex items-center gap-2">
			<a class="link px-2" href="https://webring.dinhe.net/prev/https://maniksharma.xyz">prev</a>
			<a class="link" href="https://webring.dinhe.net">retronaut-webring</a>
			<a class="link px-2" href="https://webring.dinhe.net/next/https://maniksharma.xyz">next</a>
		</div>

		<div class="flex items-center gap-2">
			<a class="link px-2" href="https://hotlinewebring.club/beigestack/previous">prev</a>
			<a class="link" href="https://hotlinewebring.club">hotline-webring</a>
			<a class="link px-2" href="https://hotlinewebring.club/beigestack/next">next</a>
		</div>

		<a href="http://internetometer.com/give/51711"
			><img src="http://internetometer.com/image/51711.png" alt="internetometer" /></a
		>

		<div class="flex gap-2">
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
		></iframe>

		<div id="apartment-webring"></div>
		<div id="aperturewebring">
			<noscript>
				This site is part of the <a
					href="https://jack-dawlia.neocities.org/page/shrines/portal/aperturewebring"
					>Aperture Webring</a
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

	<hr class="w-[80%] my-4 opacity-30" />

	<div class="mt-2 flex gap-4 font-[Jetbrains_Mono]">
		<a class="link" href="/">/</a>
		<a class="link" href="/about">/about</a>
		<a class="link" href="/blog">/blog</a>
		<a class="link" href="/projects">/projects</a>
		<a class="font-bold link" href="/webrings">sillies</a>
		<a class="link" href="/misc">/misc</a>
	</div>
</main>
