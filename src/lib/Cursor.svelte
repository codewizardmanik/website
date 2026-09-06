<script lang="ts">
	import { onMount } from 'svelte';

	let x = $state(0);
	let y = $state(0);
	let ringX = $state(0);
	let ringY = $state(0);
	let text = $state('');

	onMount(() => {
		const handleMove = (e: MouseEvent) => {
			x = e.clientX;
			y = e.clientY;

			const target = e.target as HTMLElement;
			const cursor = target.closest('[data-cursor]') as HTMLElement | null;

			text = cursor?.dataset.cursor ?? '';
		};

		window.addEventListener('mousemove', handleMove);

		let animationFrame: number;

		const animate = () => {
			ringX += (x - ringX) * 0.15;
			ringY += (y - ringY) * 0.15;

			animationFrame = requestAnimationFrame(animate);
		};

		animationFrame = requestAnimationFrame(animate);

		return () => {
			window.removeEventListener('mousemove', handleMove);
			cancelAnimationFrame(animationFrame);
		};
	});
</script>

<div class="cursor-dot" style:transform={`translate(${x}px, ${y}px)`}></div>

<div
	class="cursor-ring"
	class:active={text !== ''}
	style:transform={`translate(${ringX}px, ${ringY}px)`}
>
	{text}
</div>

<style>
	.cursor-dot,
	.cursor-ring {
		position: fixed;
		top: 0;
		left: 0;
		pointer-events: none;
		z-index: 999999;
		border-radius: 9999px;
	}

	.cursor-dot {
		width: 6px;
		height: 6px;
		margin-left: -3px;
		margin-top: -3px;
		background: whitesmoke;
	}

	.cursor-ring {
		min-width: 24px;
		min-height: 24px;

		width: max-content;
		height: 24px;

		padding: 0 8px;

		margin-left: -12px;
		margin-top: -12px;

		display: flex;
		align-items: center;
		justify-content: center;

		border: 1px solid #16e16e;
		border-radius: 9999px;

		font-family: 'JetBrains Mono', monospace;
		font-size: 8px;
		color: #ff694b;

		white-space: nowrap;

		transition:
			width 180ms ease,
			height 180ms ease,
			margin 180ms ease,
			padding 180ms ease,
			border-color 180ms ease,
			background 180ms ease;
	}

	.cursor-ring.active {
		min-width: 40px;
		min-height: 40px;

		width: max-content;
		height: 40px;

		margin-left: -20px;
		margin-top: -20px;

		padding: 0 14px;

		color: whitesmoke;
		font-size: small;

		border-color: #ff694b;
		background: #ff694b;
	}

	@media (hover: none), (pointer: coarse) {
		.cursor-dot,
		.cursor-ring {
			display: none;
		}
	}
</style>
