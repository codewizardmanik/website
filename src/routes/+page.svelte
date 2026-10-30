<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';

	const quotes = [
		'aka a developer',
		'aka a goofy guy',
		'aka a student',
		'aka a.. what?',
		'aka a neeeeeeeeeeeerd',
		'aka an exception(e)'
	];

	let quote = $state(quotes[0]);
	let lastIndex = 0;
	let message = $state('');

	let main: HTMLElement;
	let identity: HTMLElement;
	let about: HTMLAnchorElement;
	let projects: HTMLAnchorElement;
	let blog: HTMLAnchorElement;
	let sillies: HTMLAnchorElement;
	let svg: SVGSVGElement;

	let paths = $state(['', '', '', '']);
	let mouse = { x: -1000, y: -1000 };
	let returnTimer: ReturnType<typeof setTimeout>;
	let resizeObserver: ResizeObserver;

	function updateRopes() {
		if (!main || !identity || !svg) return;

		const root = main.getBoundingClientRect();
		const centre = identity.getBoundingClientRect();
		const links = [about, projects, blog, sillies];

		svg.setAttribute('viewBox', `0 0 ${root.width} ${root.height}`);

		const cx = centre.left - root.left + centre.width / 2;
		const cy = centre.top - root.top + centre.height / 2;

		paths = links.map((link, index) => {
			if (!link) return '';

			const rect = link.getBoundingClientRect();
			const bx = rect.left - root.left + rect.width / 2;
			const by = rect.top - root.top + rect.height / 2;

			const dx = bx - cx;
			const dy = by - cy;
			const length = Math.hypot(dx, dy) || 1;

			function boundary(
				x: number,
				y: number,
				width: number,
				height: number,
				vx: number,
				vy: number
			) {
				const scale =
					1 /
					Math.max(
						Math.abs(vx) / Math.max(width / 2, 1),
						Math.abs(vy) / Math.max(height / 2, 1),
						0.001
					);

				return { x: x + vx * scale, y: y + vy * scale };
			}

			const start = boundary(cx, cy, centre.width, centre.height, dx / length, dy / length);
			const end = boundary(bx, by, rect.width, rect.height, -dx / length, -dy / length);

			const vx = end.x - start.x;
			const vy = end.y - start.y;
			const distance = Math.hypot(vx, vy) || 1;

			const nx = -vy / distance;
			const ny = vx / distance;

			const bends = [-32, -32, 19, -27];
			let bend = bends[index];

			const mx = mouse.x;
			const my = mouse.y;
			const midX = (start.x + end.x) / 2;
			const midY = (start.y + end.y) / 2;

			const mdx = midX - mx;
			const mdy = midY - my;
			const mouseDistance = Math.hypot(mdx, mdy);

			if (mouseDistance < 145 && mouseDistance > 0) {
				const proximity = 1 - mouseDistance / 145;
				const strength = proximity * proximity * 35;
				bend += (mdx * nx + mdy * ny >= 0 ? 1 : -1) * strength;
			}

			const c1x = start.x + vx * 0.3 + nx * bend - (index === 0 ? 4 : 0);
			const c1y = start.y + vy * 0.3 + ny * bend;
			const c2x = start.x + vx * 0.8 + nx * bend * 0.65 - (index === 0 ? 4 : 0);
			const c2y = start.y + vy * 0.6 + ny * bend * 0.65;

			return `M ${start.x} ${start.y} C ${c1x} ${c1y}, ${c2x} ${c2y}, ${end.x} ${end.y}`;
		});
	}

	function handleMouseMove(event: MouseEvent) {
		const rect = main.getBoundingClientRect();

		mouse = {
			x: event.clientX - rect.left,
			y: event.clientY - rect.top
		};

		updateRopes();
	}

	function handleMouseLeave() {
		clearTimeout(returnTimer);

		const start = performance.now();
		const duration = 350;
		const from = { ...mouse };

		function animateReturn(now: number) {
			const progress = Math.min((now - start) / duration, 1);
			const eased = 1 - Math.pow(1 - progress, 3);

			mouse = {
				x: from.x + (-1000 - from.x) * eased,
				y: from.y + (-1000 - from.y) * eased
			};

			updateRopes();

			if (progress < 1) {
				returnTimer = setTimeout(() => requestAnimationFrame(animateReturn), 16);
			}
		}

		requestAnimationFrame(animateReturn);
	}

	function sendMessage(event: SubmitEvent) {
		event.preventDefault();

		const form = event.currentTarget as HTMLFormElement;
		const textarea = form.querySelector('textarea');
		const nameInput = form.querySelector<HTMLInputElement>('.message-name');

		if (!textarea?.value.trim() || !nameInput?.value.trim()) return;

		window.location.href =
			`mailto:headhoncho@maniksharma.xyz?subject=${encodeURIComponent('something from your website')}` +
			`&body=${encodeURIComponent(`${textarea.value.trim()}\n\n-${nameInput.value.trim()}`)}`;
	}

	onMount(() => {
		let frame = 0;

		const interval = setInterval(() => {
			let index: number;

			do {
				index = Math.floor(Math.random() * quotes.length);
			} while (index === lastIndex);

			lastIndex = index;
			quote = quotes[index];
		}, 3500);

		resizeObserver = new ResizeObserver(() => {
			cancelAnimationFrame(frame);
			frame = requestAnimationFrame(updateRopes);
		});

		resizeObserver.observe(main);
		resizeObserver.observe(identity);

		[about, projects, blog, sillies].forEach((element) => {
			if (element) resizeObserver.observe(element);
		});

		window.addEventListener('resize', updateRopes);
		frame = requestAnimationFrame(updateRopes);

		return () => {
			clearInterval(interval);
			clearTimeout(returnTimer);
			resizeObserver.disconnect();
			window.removeEventListener('resize', updateRopes);
			cancelAnimationFrame(frame);
		};
	});
</script>

<svelte:head>
	<title>this is the website of {quote.replace(/^aka\s+/, '')}</title>
	<meta name="theme-color" content="#000000" />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700&family=Instrument+Serif:ital@0;1&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main
	bind:this={main}
	class="home no-scrollbar"
	onmousemove={handleMouseMove}
	onmouseleave={handleMouseLeave}
>
	<svg bind:this={svg} class="ropes" aria-hidden="true">
		{#each paths as path, i}
			<g class="rope" class:rope-hover={false} key={i}>
				<path class="rope-shadow" d={path} />
				<path class="rope-base" d={path} />
				<path class="rope-highlight" d={path} />
			</g>
		{/each}
	</svg>

	<div class="identity" bind:this={identity}>
		<div class="hi">hi, im</div>
		<img
			class="transition-transform duration-300 hover:scale-[1.05]"
			alt="manik sharma"
			src="logotype.png"
		/>
		<div class="quote">
			{#key quote}
				<span transition:fly={{ y: 12, duration: 300 }}>
					{quote}
				</span>
			{/key}
		</div>
	</div>

	<a
		bind:this={about}
		class="orbit-link about"
		href="/about"
		data-cursor="i do a lot of random stuff. im (currently) a 14 year old student."
	>
		/about
	</a>

	<a
		bind:this={projects}
		class="orbit-link projects"
		href="/projects"
		data-cursor="PROJECTS (all oss)"
	>
		/projects
	</a>

	<a
		bind:this={blog}
		class="orbit-link blog"
		href="/blog"
		data-cursor="BLOG (and alotta writing for funsies <3)"
	>
		/blog
	</a>

	<a
		bind:this={sillies}
		class="orbit-link sillies"
		href="/webrings"
		data-cursor=":3 (webrings and moar)"
	>
		sillies
	</a>

	<div class="song-orbit">
		<div class="song-label">goated song:</div>
		<div class="song-card">
			<a
				href="https://open.spotify.com/track/3DK6m7It6Pw857FcQftMds"
				target="_blank"
				rel="noopener noreferrer"
				class="song-cover"
				aria-label="Listen to Runaway on Spotify"
			>
				<img
					src="https://image-cdn-fa.spotifycdn.com/image/ab67616d00001e02d9194aa18fa4c9362b47464f"
					alt="Runaway single cover by Kanye West"
				/>
			</a>

			<div class="song-info">
				<a
					href="https://open.spotify.com/track/3DK6m7It6Pw857FcQftMds"
					target="_blank"
					rel="noopener noreferrer"
				>
					<div class="song-title">runaway</div>
				</a>
				<a
					href="https://open.spotify.com/artist/2eZZVwzCJsugkoiKUlMls9"
					target="_blank"
					rel="noopener noreferrer"
				>
					<div class="song-artist">kanye west</div>
				</a>
			</div>
		</div>
	</div>

	<form class="message-box" onsubmit={sendMessage}>
		<div class="message-heading">send me something!</div>
		<textarea
			aria-label="Your message"
			maxlength="60"
			class="focus:outline-none focus:ring-0 text-[#ff69b4] bg-transparent placeholder-[#ff69b4] font-['Funnel_Display']"
			required
			bind:value={message}
			onkeydown={(e) => {
				if (e.key === 'Enter') e.preventDefault();
			}}></textarea>
		<input
			type="text"
			class="text-xl message-name bg-transparent underline decoration-[#16e16e] text-[#ff69b4] focus:outline-none focus:ring-0 placeholder-[#ff69b4]"
			placeholder="your name"
			required
			maxlength="25"
		/>
		<button type="submit">send it straight to me!</button>
	</form>

	<div class="club-info -mb-5">
		<p>
			im part of my schools tech club (well 2 of them),
			<a
				href="https://robonexus46.vercel.app/"
				data-cursor="ROBONEXUS"
				target="_blank"
				rel="noreferrer"
			>
				robonexus
			</a>
			and
			<a
				href="https://techsyndicate.us"
				data-cursor="TECH SYNDICATE"
				target="_blank"
				rel="noreferrer"
			>
				tech syndicate
			</a>
		</p>
	</div>

	<nav class="socials" aria-label="Social links">
		<a href="https://github.com/codewizardmanik" target="_blank" rel="noreferrer">github</a>
		<a href="https://www.youtube.com/@codewizardmanik" target="_blank" rel="noreferrer">yt</a>
		<a href="https://www.instagram.com/m4n1k.sh/" target="_blank" rel="noreferrer">ig</a>
		<a href="mailto:headhoncho@maniksharma.xyz">email</a>
		<a href="https://www.linkedin.com/in/manik-sharma-30b4a9419/" target="_blank" rel="noreferrer"
			>linkedin</a
		>
		<a href="https://vncl.xyz" target="_blank" rel="noreferrer">""company"" website</a>
	</nav>

	<div class="all-links">
		all my links @
		<a href="https://links.maniksharma.xyz" target="_blank" rel="noreferrer">
			https://links.maniksharma.xyz
		</a>
	</div>
</main>

<style>
	:global(*) {
		box-sizing: border-box;
	}

	:global(html) {
		background: #000;
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		background: #000;
		color: #fff;
		font-family: 'Funnel Display', sans-serif;
	}

	:global(::selection) {
		background: #16e16e;
		color: #000;
	}

	.home {
		--pink: #ff69b4;
		--green: #16e16e;
		position: relative;
		width: 100%;
		height: 100svh;
		min-height: 600px;
		overflow: hidden;
		background: #000;
	}

	.ropes {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		overflow: visible;
		pointer-events: none;
		z-index: 1;
	}

	.rope path {
		fill: none;
		stroke-linecap: round;
		stroke-linejoin: round;
		vector-effect: non-scaling-stroke;
	}

	.rope-shadow {
		stroke: #ff69b4;
		stroke-width: 7;
		opacity: 0.12;
		filter: blur(4px);
	}

	.rope-base {
		stroke: #ff69b4;
		stroke-width: 3;
		opacity: 0.9;
	}

	.rope-highlight {
		stroke: #ffb0d8;
		stroke-width: 1;
		opacity: 0.7;
		stroke-dasharray: 3 8;
	}

	.identity {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		width: 240px;
		text-align: center;
		z-index: 3;
	}

	.hi {
		position: absolute;
		left: 8px;
		top: -28px;
		font-size: 23px;
	}

	h1 {
		margin: 0;
		color: var(--green);
		font-family: 'Instrument Serif', serif;
		font-size: clamp(72px, 7vw, 100px);
		font-weight: 400;
		line-height: 0.95;
		letter-spacing: -2px;
		transition:
			letter-spacing 0.3s ease,
			text-shadow 0.3s ease;
		cursor: default;
	}

	.identity:hover h1 {
		letter-spacing: 1px;
		text-shadow: 0 0 22px #16e16e30;
	}

	.quote {
		height: 35px;
		margin-top: 12px;
		overflow: hidden;
		color: var(--pink);
		font-family: 'Instrument Serif', serif;
		font-size: 25px;
		white-space: nowrap;
	}

	.quote span {
		display: block;
	}

	.orbit-link {
		position: absolute;
		z-index: 4;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 13px 15px;
		border: 2.5px solid var(--pink);
		border-radius: 29px;
		background: #000;
		color: var(--green);
		font-size: clamp(22px, 2.1vw, 34px);
		text-decoration: underline;
		text-underline-offset: 4px;
		transition:
			transform 0.3s cubic-bezier(0.2, 0.8, 0.2, 1),
			background 0.3s ease,
			box-shadow 0.3s ease,
			border-radius 0.3s ease;
	}

	.orbit-link:hover {
		transform: scale(1.09) rotate(-3deg);
		background: #080008;
		box-shadow: 0 0 24px #ff69b41c;
		border-radius: 19px;
	}

	.about {
		left: 15.5%;
		top: 18.2%;
	}
	.projects {
		left: 65.8%;
		top: 24.2%;
	}
	.blog {
		left: 27.4%;
		top: 67.5%;
	}
	.sillies {
		left: 68.3%;
		top: 65.8%;
	}

	.song-orbit {
		position: absolute;
		left: 1%;
		top: 75.5%;
		z-index: 4;
		animation: wonky-orbit 19s ease-in-out infinite;
	}

	.song-label {
		margin-bottom: 5px;
		color: var(--pink);
		font-size: 20px;
	}

	.song-card {
		display: flex;
		align-items: stretch;
		gap: 10px;
		width: max-content;
		max-width: 100%;
	}

	.song-cover {
		display: block;
		flex: 0 0 56px;
		width: 56px;
		align-self: stretch;
		overflow: hidden;
		border-radius: 4px;
	}

	.song-cover img {
		display: block;
		width: 100%;
		height: 100%;
		min-height: 100%;
		object-fit: cover;
	}

	.song-info {
		display: flex;
		flex-direction: column;
		justify-content: center;
		min-width: 0;
	}

	.song-title {
		display: block;
		width: max-content;
		max-width: 100%;
		color: var(--green);
		font-size: clamp(20px, 2vw, 32px);
		line-height: 1.1;
		text-decoration: underline;
		text-underline-offset: 3px;
		transition: color 0.2s ease;
	}

	.song-title:hover,
	.song-artist:hover {
		color: #fff;
	}

	.song-artist {
		width: max-content;
		max-width: 100%;
		margin-top: 4px;
		color: var(--pink);
		font-size: 15px;
		text-decoration: underline;
	}

	@keyframes wonky-orbit {
		0%,
		100% {
			transform: translate(0, 0) rotate(0);
		}
		13% {
			transform: translate(25px, -13px) rotate(2deg);
		}
		26% {
			transform: translate(65px, 8px) rotate(-2deg);
		}
		39% {
			transform: translate(105px, -22px) rotate(1deg);
		}
		53% {
			transform: translate(125px, 9px) rotate(-1deg);
		}
		67% {
			transform: translate(83px, 20px) rotate(2deg);
		}
		81% {
			transform: translate(37px, 5px) rotate(-2deg);
		}
		92% {
			transform: translate(12px, -17px) rotate(1deg);
		}
	}

	.message-box {
		position: absolute;
		top: 2.6%;
		right: 0.6%;
		z-index: 5;
		display: flex;
		flex-direction: column;
		width: 235px;
		height: 408px;
		overflow: hidden;
		border: 5px solid var(--pink);
		border-radius: 25px;
		background: #000;
		color: var(--green);
		font-family: 'Instrument Serif', serif;
	}

	.message-heading {
		display: flex;
		align-items: center;
		justify-content: center;
		min-height: 63px;
		padding: 8px 3px;
		border-bottom: 5px solid var(--pink);
		font-size: 25px;
		white-space: nowrap;
	}

	.message-box textarea {
		flex: 1;
		width: 100%;
		min-height: 0;
		resize: none;
		padding: 10px;
		border: 0;
		outline: 0;
		background: #000;
		color: var(--green);
		font:
			19px 'Funnel Display',
			sans-serif;
		line-height: 38px;
		background-image: repeating-linear-gradient(
			to bottom,
			transparent 0,
			transparent 38px,
			var(--green) 39px,
			var(--green) 40px
		);
	}

	textarea {
		scrollbar-width: none;
		resize: none;
		border-bottom: 5px solid var(--pink);
	}

	textarea::-webkit-scrollbar {
		display: none;
	}

	.message-box textarea:focus {
		background-color: #071009;
	}

	.message-name {
		width: 100%;
		min-height: 42px;
		padding: 5px 10px;
		border: 0;
		border-top: 2px solid var(--pink);
		border-bottom: 2px solid var(--green);
		outline: 0;
	}

	.message-box button {
		min-height: 53px;
		padding: 5px 2px;
		border: 0;
		border-top: 5px solid var(--pink);
		background: #000;
		color: var(--green);
		font:
			25px 'Instrument Serif',
			serif;
		white-space: nowrap;
		cursor: pointer;
		transition:
			background 0.2s ease,
			color 0.2s ease;
	}

	.message-box button:hover {
		background: var(--pink);
		color: #000;
	}

	.club-info {
		position: absolute;
		right: 2.3%;
		bottom: 10%;
		z-index: 4;
		max-width: 65%;
		color: #a3a3a3;
		font-size: 13px;
		text-align: right;
		line-height: 1.4;
	}

	.club-info p {
		margin: 0;
	}

	.club-info a {
		color: var(--green);
	}

	.club-info a:hover {
		text-decoration: underline;
	}

	.socials {
		position: absolute;
		right: 2.3%;
		bottom: 4.5%;
		z-index: 4;
		display: flex;
		align-items: center;
		justify-content: flex-end;
		flex-wrap: wrap;
		gap: 6px 16px;
		max-width: 65%;
		color: #a3a3a3;
		font-size: 16px;
		line-height: 1.4;
	}

	.socials a {
		color: #a3a3a3;
		text-decoration: none;
		transition: color 0.2s ease;
	}

	.socials a:hover {
		color: var(--green);
	}

	.all-links {
		position: absolute;
		right: 2.3%;
		bottom: 1.5%;
		z-index: 4;
		color: #a3a3a3;
		font-size: 13px;
		text-align: right;
	}

	.all-links a {
		color: var(--green);
		text-decoration: underline;
		text-underline-offset: 2px;
	}

	.no-scrollbar {
		scrollbar-width: none;
	}

	.no-scrollbar::-webkit-scrollbar {
		display: none;
	}

	@media (prefers-reduced-motion: reduce) {
		.song-orbit {
			animation: none;
		}
	}

	@media (max-width: 700px) {
		.home {
			height: auto;
			min-height: 100svh;
			overflow-x: hidden;
			overflow-y: auto;
			padding: 35px 20px;
			display: flex;
			flex-direction: column;
			align-items: center;
			gap: 25px;
		}

		.ropes {
			display: none;
		}

		.identity {
			position: relative;
			left: auto;
			top: auto;
			transform: none;
			width: 100%;
			margin: 35px 0 12px;
		}

		h1 {
			font-size: 100px;
		}

		.hi {
			left: calc(50% - 90px);
		}

		.orbit-link {
			position: relative;
			left: auto;
			top: auto;
			font-size: 25px;
		}

		.about,
		.blog {
			align-self: flex-start;
		}
		.projects,
		.sillies {
			align-self: flex-end;
		}

		.song-orbit {
			position: relative;
			left: auto;
			top: auto;
			align-self: flex-start;
			animation: none;
		}

		.song-card {
			max-width: 100%;
		}

		.song-cover {
			flex-basis: 56px;
			width: 56px;
			height: 56px;
		}

		.message-box {
			position: relative;
			top: auto;
			right: auto;
			width: min(280px, 100%);
			height: 280px;
			align-self: flex-end;
		}

		.club-info {
			position: relative;
			right: auto;
			bottom: auto;
			max-width: 100%;
			text-align: center;
			font-size: 13px;
		}

		.socials {
			position: relative;
			right: auto;
			bottom: auto;
			max-width: 100%;
			justify-content: center;
			font-size: 14px;
			color: #a3a3a3 !important;
		}

		.all-links {
			position: relative;
			right: auto;
			bottom: auto;
			text-align: center;
			font-size: 12px;
			overflow-wrap: anywhere;
		}
	}
</style>
