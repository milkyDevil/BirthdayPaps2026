<script lang="ts">
	import { resolve } from '$app/paths';

	type Card = {
		image: `/${string}`;
		caption: string;
		message: string;
	};

	let cards = $state<Card[]>([
		{
			image: '/cards/paps_overall.png',
			caption: 'The day we met ❤️',
			message: 'I still remember how everything felt magical.'
		},
		{
			image: '/cards/paps_parents.png',
			caption: 'Our favorite memory ✨',
			message: 'Every moment with you is my favorite story.'
		},
		{
			image: '/cards/paps_sisters.png',
			caption: 'Today 🎂',
			message: 'Happy Birthday to the most special person in my life.'
		}
	]);

	let currentIndex = $state(0);
	let flipped = $state(false);

	let startX = 0;
	let startY = 0;

	const r = resolve as (p: `/${string}`) => string;

	function nextCard() {
		if (currentIndex < cards.length - 1) {
			currentIndex++;
			flipped = false;
		}
	}

	function prevCard() {
		if (currentIndex > 0) {
			currentIndex--;
			flipped = false;
		}
	}

	function toggleFlip() {
		flipped = !flipped;
	}

	function onTouchStart(e: TouchEvent) {
		startX = e.changedTouches[0].clientX;
		startY = e.changedTouches[0].clientY;
	}

	function onTouchEnd(e: TouchEvent) {
		const dx = e.changedTouches[0].clientX - startX;
		const dy = e.changedTouches[0].clientY - startY;

		if (Math.abs(dx) > Math.abs(dy)) {
			if (Math.abs(dx) > 40) toggleFlip();
		} else {
			if (dy < -40) nextCard();
			if (dy > 40) prevCard();
		}
	}
</script>

<button
	type="button"
	class="fixed inset-0 flex touch-none items-center justify-center overflow-hidden bg-black select-none focus:outline-none"
	ontouchstart={onTouchStart}
	ontouchend={onTouchEnd}
>
	{#key currentIndex}
		<div class="card-container">
			<div class={`card ${flipped ? 'flipped' : ''}`}>
				<!-- FRONT -->
				<div class="card-face">
					<div class="img-viewport">
						<img src={r(cards[currentIndex].image)} alt="" class="img-fit" draggable="false" />
					</div>
				</div>

				<!-- BACK -->
				<div
					class="card-face rotate-y-180 bg-linear-to-b from-purple-950 via-purple-900 to-black text-purple-200"
				>
					<div class="max-w-md space-y-6 p-8 text-center">
						<div class="text-2xl font-semibold text-purple-300">
							{cards[currentIndex].caption}
						</div>

						<div class="text-lg leading-relaxed">
							{cards[currentIndex].message}
						</div>
					</div>
				</div>
			</div>
		</div>
	{/key}

	<div class="pointer-events-none absolute bottom-6 flex gap-2">
		{#each cards as _, i}
			<div
				class={`h-2 w-2 rounded-full ${i === currentIndex ? 'bg-purple-400' : 'bg-white/30'}`}
			></div>
		{/each}
	</div>
</button>

<style>
	/* ✅ FIX 1 — force viewport height */
	.card-container {
		perspective: 1200px;
		width: 100dvw;
		height: 100dvh;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.card {
		position: relative;
		width: 100%;
		height: 100%;
		transform-style: preserve-3d;
		transition: transform 0.6s ease;
	}

	.flipped {
		transform: rotateY(180deg);
	}

	.card-face {
		position: absolute;
		inset: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		backface-visibility: hidden;
	}

	.rotate-y-180 {
		transform: rotateY(180deg);
	}

	/* ✅ FIX 2 — viewport follows card size */
	.img-viewport {
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.img-fit {
		max-width: 100%;
		max-height: 100%;
		object-fit: contain;
	}
</style>
