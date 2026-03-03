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
			caption: 'Paps: The man, the myth, the 23-year-old legend',
			message:
				'The man who is 35 on paper but 23 in his soul - this is the story of u. A journey through ur roots, ur brilliant mind, ur favourite treats, and the carefree joy u bring into every room'
		},
		{
			image: '/cards/paps_parents.png',
			caption: 'Born from a love that spans generations.',
			message:
				"Every great story has a solid foundation, and yours began with the deepest kind of love. You are the heartbeat of your home—the son who brought endless smiles and became the greatest pride and joy of your parents' lives."
		},
		{
			image: '/cards/paps_sisters.png',
			caption: "The King of Hearts... and the permanent 'Baby Bro' of the family.",
			message:
				'Growing up as the only brother to five sisters means you were never short on love (or people to look after you!). You’ve always been their "Baby Bro"—the king of their hearts who was protected, pampered, and cheered on by your very own squad.'
		},
		{
			image: '/cards/paps_cook.png',
			caption: 'My favorite chef, serving up love one plate at a time.',
			message:
				"In our kitchen, you're the true head chef. From Italian pastas to Asian stir-frys, you have a natural gift for making everything taste incredible. It’s more than just a hobby; it’s one of the many ways you make our apartment feel like a home. Every meal you cook is a reminder of how talented (and tasty!) life with you is."
		},
		{
			image: '/cards/paps_nap.png',
			caption: 'A heart so peaceful he can fall asleep in under two minutes.',
			message:
				'While the rest of the world struggles with insomnia, you’ve mastered the ultimate superpower. Whether you\'re lying down for a "quick" YouTube video or just resting for a minute, you find dreamland in record time. It’s a peace of mind that I find both hilarious and absolutely adorable.'
		},
		{
			image: '/cards/paps_sneakers.png',
			caption: 'Life is too short for boring shoes.',
			message:
				'Your world is a vibrant rainbow, especially when it comes to your feet! You have an absolute passion for multi-colored, low-top canvas sneakers. While they might not last forever, they certainly bring endless energy and a pop of joyful color to every step of your journey.'
		},
		{
			image: '/cards/paps_food.png',
			caption: 'A world of flavor, one plate at a time.',
			message:
				'Your appetite for life is as diverse as your palate! Whether it’s a perfectly cooked medium-rare steak, the spicy kick of Naga food, or the comforting flavors of Assamese and Japanese cuisines, you are a true explorer of taste. From sushi and ramen to pizza and boiled veggies, there’s rarely a dish you don’t appreciate—making every meal with you a delicious new adventure.'
		},
		{
			image: '/cards/paps_knowledge.png',
			caption: 'A true lover of knowledge, one concept at a time.',
			message:
				"Your mind is a vast landscape of curiosity, where coding in JavaScript and Vue meets the mysteries of quantum physics and thermodynamics. Whether you're diving into the complexities of mathematics, exploring the world's religions, or staying updated on global news, you are a true \"Knowledge Explorer\". You never settle for surface-level facts; you'll watch a video ten times or consult AI just to ensure you truly grasp a concept. And when you explain it back, your incredible memory and honesty—admitting when you don't know something—show your genuine love for the truth."
		},
		{
			image: '/cards/paps_coldwater.png',
			caption: 'Stay cool, stay happy, and keep on refreshing.',
			message:
				'Summer or winter, your loyalty remains with one thing: a glass of ice-cold water. You always say it’s the only real thirst quencher, the one thing that brings your body and mind true peace and happiness. Watching you enjoy your ice-cold water with such pure joy is one of those little quirks that makes you, you.'
		},
		{
			image: '/cards/paps_tea.png',
			caption: 'Never say no to tea... it’s a way of life.',
			message:
				'Whether it’s a morning ritual after a liter of water or a way to celebrate a happy moment, tea is your ultimate "heaven". You’ve mastered the art of the perfect kadak chai—three spoons of tea leaves, boiled for exactly four minutes, no extra herbs, just pure, classic flavor. You aren’t addicted, but life just feels better when a warm cup of "tea time and chill" is in your hand.'
		},
		{
			image: '/cards/paps_gossip.png',
			caption: 'Always here for the story (and the tea!).',
			message:
				'You might not be a loud social butterfly, but you are the ultimate "Active Participant" when it comes to a good story. Whether it\'s a deep debate about religion, a road trip plan, or a bit of harmless "tea" about someone’s life, you love the art of the conversation. You have this wonderful way of listening and engaging that makes every chat with friends and family feel like an event.'
		},
		{
			image: '/cards/paps_spider.png',
			caption: 'A heart of gold... and a very healthy respect for spiders.',
			message:
				'Even a "Knowledge Explorer" has one major weakness: the common wall spider. While you don\'t panic like someone seeing a cockroach, you definitely have a "security first" policy. Whether it\'s the bathroom or the bedroom, the mission is clear—Mom or I have to clear the perimeter before you\'ll step inside. It’s a healthy respect for eight-legged intruders that always keeps us on our toes!'
		},
		{
			image: '/cards/paps_toys.png',
			caption: 'Brilliant mind, baby at heart, and the king of little joys.',
			message:
				'Beneath all those complex theories and lines of code lies a heart that finds pure, unashamed joy in the simplest things. Whether we’re at a mela or a toy store, your eyes light up for the things a toddler would love—from colorful xylophones to adorable penguin and Labubu plushies. You don\'t just buy them; you cherish them, decorating your office space with dinosaurs, tiny figurines, and little "old man" toys. It’s this ability to find "Little Joys" that makes you so incredibly special to me.'
		},
		{
			image: '/cards/paps_bdaycake.png',
			caption: '1991 on paper, 23 in heart... and looks!',
			message:
				'Some people fear aging, but you simply choose to ignore it. Even as your ID says 1991, your heart (and your face!) insists on 23. With your amazing metabolism, active lifestyle—taking the stairs instead of the lift—and that slim, fit figure, you honestly make it believable. It’s a funny, sweet ritual: whenever I mention a higher number, you give me that "crying face" and remind me you’re just a guy in his early twenties.'
		},
		{
			image: '/cards/paps_me_bdaycake.png',
			caption: 'Happy 23rd Birthday! (Version 35.0)',
			message:
				'Today, I’m joining you in your favorite tradition. Forget the calendar and the "35" on the cake—today we celebrate your 23rd birthday for the twelfth time! You have the energy, the metabolism, and the fit figure to prove it. Here’s to the man who stays young by simply refusing to grow up.'
		},
		{
			image: '/cards/paps_me_hug.png',
			caption: 'Happy 23 Forever! In heart, health, and looks.',
			message:
				'My wish for you on March 6th is simple: never change. Keep your curiosity for the world, your love for kadak chai, your toy collection, and your "forever 23" heart. May your life always be as colorful as your hair and as refreshing as a glass of ice-cold water.'
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
		} else {
			currentIndex = 0;
		}
		flipped = false;
	}

	function prevCard() {
		if (currentIndex > 0) {
			currentIndex--;
		} else {
			currentIndex = cards.length - 1;
		}
		flipped = false;
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
