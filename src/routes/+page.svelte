<script lang="ts">
	type Card = {
		image: string;
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

	let currentIndex = $state<number>(0);
	let flipped = $state<boolean>(false);

	let startX = 0;
	let startY = 0;

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
	class="flex h-screen w-screen items-center justify-center overflow-hidden bg-black focus:outline-none"
	ontouchstart={onTouchStart}
	ontouchend={onTouchEnd}
	aria-label="Swipe left or right to flip. Swipe up or down to change photo."
>
	{#key currentIndex}
		<div class="card-container">
			<div class={`card ${flipped ? 'flipped' : ''}`}>
				<!-- FRONT -->
				<div class="card-face">
					<img
						src={cards[currentIndex].image}
						alt=""
						class="max-h-screen max-w-full object-contain"
						draggable="false"
					/>
				</div>

				<!-- BACK -->
				<div
					class="card-face rotate-y-180
                 bg-linear-to-b from-purple-950 via-purple-900 to-black
                 text-purple-200"
				>
					<div class="space-y-6 p-8 text-center">
						<div
							class="text-2xl font-semibold text-purple-300 drop-shadow-[0_0_12px_rgba(168,85,247,0.7)]"
						>
							{cards[currentIndex].caption}
						</div>

						<div class="text-lg leading-relaxed text-purple-200">
							{cards[currentIndex].message}
						</div>
					</div>
				</div>
			</div>
		</div>
	{/key}

	<!-- dots -->
	<div class="absolute bottom-6 flex gap-2">
		{#each cards as _, i}
			<div
				class={`h-2 w-2 rounded-full ${i === currentIndex ? 'bg-purple-400' : 'bg-white/30'}`}
			></div>
		{/each}
	</div>
</button>

<style>
	/* Only structural 3D flip styles (not visual theme) */

	.card-container {
		perspective: 1200px;
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.card {
		position: relative;
		width: 100%;
		height: 100%;
		transition: transform 0.6s ease;
		transform-style: preserve-3d;
	}

	.flipped {
		transform: rotateY(180deg);
	}

	.card-face {
		position: absolute;
		inset: 0;
		backface-visibility: hidden;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.rotate-y-180 {
		transform: rotateY(180deg);
	}
</style>
