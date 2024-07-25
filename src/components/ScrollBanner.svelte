<script lang="ts">
	import { onMount } from 'svelte';
	import birds from '../../src/lib/assets/birds.png';
	import cloud from '../../src/lib/assets/cloud.png';
	import banner from '../../src/lib/assets/banner.png';
	import vector from '../../src/lib/assets/Vector.svg';
	import banner2 from '../../src/lib/assets/banner2.png';
	import banner3 from '../lib/assets/footer-banner.png';
	let gsap, ScrollTrigger;

	onMount(async () => {
		gsap = (await import('gsap')).default;
		ScrollTrigger = (await import('gsap/ScrollTrigger')).default;

		gsap.registerPlugin(ScrollTrigger);

		// Timeline for window shields opening
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: '.scroll-container',
				start: 'top top',
				end: '+=300',
				scrub: true,
				pin: true
			}
		});

		// Animate all window shields opening
		tl.to('.window-shield', {
			yPercent: -100,
			stagger: 0.2,
			ease: 'power2.inOut'
		});

		// Create a ScrollTrigger for the airplane-interior
		ScrollTrigger.create({
			trigger: '.content-section',
			start: 'top bottom',
			onEnter: () => {
				document.getElementById('airplane-interior').style.position = 'relative';
			},
			onLeaveBack: () => {
				document.getElementById('airplane-interior').style.position = 'sticky';
			}
		});

		gsap.utils.toArray('[data-speed]').forEach((el) => {
			const speed = parseFloat(el.getAttribute('data-speed'));
			const offsetY = parseFloat(el.getAttribute('data-offset-y') || '0');
			const amplitude = parseFloat(el.getAttribute('data-amplitude') || '50');

			gsap.to(el, {
				x: () => (1 - speed) * ScrollTrigger.maxScroll(window),
				y: () => Math.sin(ScrollTrigger.maxScroll(window) * 0.001) * amplitude + offsetY,
				ease: 'none',
				scrollTrigger: {
					start: 0,
					end: 'max',
					invalidateOnRefresh: true,
					scrub: 0.5
				}
			});
		});
	});
</script>

<!-- Main Content -->
<div class="scroll-container w-full flex flex-col items-center">
	<div
		id="airplane-interior"
		class="airplane-interior w-full h-screen bg-gray-300 flex justify-center items-center overflow-hidden sticky top-0"
	>
		<img
			src={birds}
			data-speed="0.25"
			data-amplitude="30"
			data-offset-y="20"
			alt="bird"
			class="bg-blend-screen absolute top-32 left-[20%] sm:left-[40%] z-10 h-32"
		/>
		<img
			src={cloud}
			data-speed="0.50"
			data-amplitude="15"
			data-offset-y="-10"
			alt="cloud"
			class="bg-blend-screen cloud absolute top-28 left-[10%] sm:left-[30%] z-10 h-32"
		/>
		<svg class="background-circle" width="1000" height="1000" viewBox="0 0 800 800">
			<circle cx="400" cy="400" r="380" fill="none" stroke="#e0e0e0" stroke-width="1" />
			<circle cx="400" cy="400" r="300" fill="none" stroke="#e0e0e0" stroke-width="1" />
			<circle cx="400" cy="400" r="210" fill="none" stroke="#e0e0e0" stroke-width="1" />
			<circle cx="400" cy="400" r="150" fill="none" stroke="#e0e0e0" stroke-width="1" />
		</svg>
		<div class="window-row flex gap-40">
			<div class="flight-window hidden lg:flex">
				<div class="window-frame">
					<div class="window-glass">
						<div class="window-image window-image-1"></div>
						<div class="window-shield"></div>
					</div>
				</div>
			</div>
			<div class="flight-window">
				<div class="window-frame">
					<div class="window-glass">
						<div class="window-image window-image-2"></div>
						<div class="window-shield"></div>
					</div>
				</div>
			</div>
			<div class="flight-window hidden sm:flex">
				<div class="window-frame">
					<div class="window-glass">
						<div class="window-image window-image-3"></div>
						<div class="window-shield"></div>
					</div>
				</div>
			</div>
		</div>
		<section class="absolute bottom-32 leading-4 text-center space-y-3">
			<h1 class="text-[1.5rem] leading-4 font-bold text-blue-600">Attention Passengers!</h1>
			<p class="text-lg text-white font-medium leading-6">
				Your journey is about to begin <br />
				Please Ensure Your Seatbelts are Fastened
			</p>
		</section>
	</div>
	<nav class="navbar relative bg-[#155DFF] w-full py-4 z-10 shadow-sm">
		<div class="container mx-auto flex justify-between items-center p-4">
			<a href="#" class="text-white text-2xl font-bold">Airline</a>
			<ul class=" space-x-6 hidden sm:flex">
				<li><a href="#home" class="text-white hover:text-blue-300">Home</a></li>
				<li><a href="#about" class="text-white hover:text-blue-300">About</a></li>
				<li><a href="#services" class="text-white hover:text-blue-300">Services</a></li>
				<li><a href="#contact" class="text-white hover:text-blue-300">Contact</a></li>
			</ul>
		</div>
	</nav>
	<div class="content-section-section w-full relative">
		<!-- Navbar -->
		<img src={banner} alt="banner" class="w-full" loading="lazy" />
		<h1
			class="absolute text-[2rem] sm:text-[4rem] z-10 top-[4%] sm:top-[20%] flex mx-6 sm:mx-24 font-bold text-white leding-4 sm:leading-[5rem]"
		>
			Mastering Your <br />Journey
		</h1>

		<section class="relative header-section w-full flex justify-center items-center">
			<div class="absolute left-0 top-0 z-0">
				<img src={vector} alt="banner" class="w-12 h-12 sm:w-32 sm:h-36" loading="lazy" />
			</div>
			<section class="flex flex-col items-center py-4 sm:py-8">
				<h1
					class="z-20 text-xl sm:text-4xl font-bold mb-4 capitalize text-[#155DFF] w-full text-center leading-12"
				>
					Explore Through Busy CitySacpes <br /> and Exotic Natural Landsscapes
				</h1>
				<p class="text-slate-600 py-0 px-2 sm:px-0 sm:py-4 text-center">
					Experience the best of both worlds and beyond with Sky Guru.
				</p>
			</section>
		</section>
		<div class="flex justify-center flex-wrap gap-4 w-full content-center my-4">
			<div class="text-center rounded-lg shadow-xl w-64 sm:w-auto">
				<img
					src="https://images.unsplash.com/photo-1433256392503-913cee5877e3"
					loading="lazy"
					alt="Cityscape"
					class="w-full h-60 mb-2 rounded"
				/>
				<div class="p-4 break-words">
					<h3 class="font-semibold">Cityscapes</h3>
					<p>Marvel at urban landscapes from the sky</p>
				</div>
			</div>
			<div class="text-center rounded-lg shadow-xl w-64 sm:w-auto">
				<img
					src="https://images.unsplash.com/photo-1434873740857-1bc5653afda8"
					loading="lazy"
					alt="Cloudscape"
					class="w-full h-60 mb-2 rounded"
				/>
				<div class="p-4 break-words">
					<h3 class="font-semibold">Cloudscapes</h3>
					<p>Float through majestic cloud formations</p>
				</div>
			</div>
			<div class="text-center rounded-lg shadow-xl w-64 sm:w-auto">
				<img
					src="https://images.unsplash.com/photo-1439684717901-bbeeade9a9f2"
					loading="lazy"
					alt="Sunset"
					class="w-full h-60 mb-2 rounded"
				/>
				<div class="p-4 break-words">
					<h3 class="font-semibold">Sunsets</h3>
					<p>Witness breathtaking sunsets above the clouds</p>
				</div>
			</div>
		</div>
	</div>

	<!-- container -->
	<div class="flex relative flex-wrap gap-4 w-full my-6">
		<img src={banner2} alt="banner" class=" w-full h-[15rem] sm:h-[35rem]" />
		<div class="absolute text-center top-10 sm:top-20 flex flex-col w-full justify-center">
			<h1 class="text-4xl text-white z-10 leding-7 font-bold">Why?</h1>
			<p class="text-white leading-9">
				Vacations are special, and you deserve to spend them <br />the right way!
			</p>
		</div>
		<div
			class="relative sm:absolute flex bottom-16 justify-center items-center sm:-bottom-52 w-full flex-wrap"
		>
			<section
				class="z-10 flex flex-col sm:flex-row w-full items-center sm:items-start gap-10 justify-center"
			>
				<div
					class="text-center rounded-lg shadow-xl bg-white w-72 h-auto sm:h-[30rem] border border-slate-500/20"
				>
					<img
						src="https://images.unsplash.com/photo-1433256392503-913cee5877e3"
						loading="lazy"
						alt="Cityscape"
						class="w-full h-60 mb-2 rounded"
					/>

					<div class="p-4 break-words text-start">
						<h3 class="font-semibold text-[#155DFF]">Best Service</h3>
						<p class="text-slate-500">
							Beyond just a trip; we are all about crafting unforgettable experiences. With our warm
							smiles and personalized attention, every moment of your journey is
						</p>
					</div>
				</div>
				<div
					class="text-center rounded-lg shadow-xl bg-white w-72 h-auto sm:h-[30rem] border border-slate-500/20"
				>
					<img
						src="https://images.unsplash.com/photo-1434873740857-1bc5653afda8"
						loading="lazy"
						alt="Cloudscape"
						class="w-full h-60 mb-2 rounded"
					/>
					<div class="p-4 break-words text-start">
						<h3 class="font-semibold text-[#155DFF]">Best Price Assurance</h3>
						<p class="text-slate-500">
							Worried about breaking the bank? Fear not! At Sky Guru Travels, we promise the best
							prices for your dream adventures. Get ready for unbeatable deals without compromising
							on quality.
						</p>
					</div>
				</div>
				<div
					class="text-center rounded-lg shadow-xl bg-white w-72 h-auto sm:h-[30rem] border border-slate-500/20"
				>
					<img
						src="https://images.unsplash.com/photo-1439684717901-bbeeade9a9f2"
						loading="lazy"
						alt="Sunset"
						class="w-full h-60 mb-2 rounded"
					/>
					<div class="p-4 break-words text-start">
						<h3 class="font-semibold text-[#155DFF]">Best Lodging Choices</h3>
						<p class="text-slate-500">
							From cozy hideaways to luxurious resorts, we've handpicked the finest accommodations
							just for you. Rest easy knowing that wherever you lay your head, it'll be a perfect
							match for your style and comfort.
						</p>
					</div>
				</div>
			</section>
		</div>
	</div>

	<!-- section 2 -->
	<section class="relative flex flex-col items-center py-4 sm:py-8 mt-0 sm:mt-52">
		<h1
			class="z-20 text-xl sm:text-4xl font-bold mb-4 capitalize text-[#155DFF] w-full text-center leading-12"
		>
			Our Tour Buddies
		</h1>
		<p class="text-slate-600 py-0 px-2 sm:px-0 sm:py-4 w-10/12 sm:w-6/12 text-center">
			Meet our fantastic partners of adventure enthusiasts, ready to turn your travel dreams into
			unforgettable memories. Let's kick off an epic journey together!
		</p>
	</section>
</div>

<!-- footer banner -->

<section class="w-full h-48 relative">
	<img src="{banner3}" alt="banner" class="h-56 sm:h-96 w-full" />
	<div class="absolute top-10 flex flex-col w-full justify-center items-center space-y-5">
		<section class="flex flex-col justify-center items-center">
			<h1 class="font-bold text-white text-xl sm:text-4xl">Subscribe Now for Best Deals</h1>
			<p class="text-white py-4">Become the First to Know about Our Best Offers!</p>
		</section>
		<div
			class="bg-white w-5/6 sm:w-4/12 h-12 rounded-full justify-between overflow-hidden flex items-center"
		>
			<input
				type="email"
				class="text-start h-full outline-none overflow-hidden px-4"
				placeholder="Type your email here"
				name=""
				id=""
			/>
			<button class="rounded-full w-32 h-5/6 bg-[#155DFF] text-white mr-[3px]"> Subscribe</button>
		</div>
	</div>
</section>

<style>
	.navbar a {
		text-decoration: none;
	}

	.navbar a:hover {
		text-decoration: underline;
	}

	.background-circle {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}

	.airplane-interior {
		position: sticky;
		top: 0;
		background: rgb(26, 14, 22);
		background: -moz-radial-gradient(
			circle,
			rgba(26, 14, 22, 1) 0%,
			rgba(185, 184, 185, 1) 0%,
			rgba(194, 197, 226, 0.8995973389355743) 61%,
			rgba(229, 243, 252, 1) 100%
		);
		background: -webkit-radial-gradient(
			circle,
			rgba(26, 14, 22, 1) 0%,
			rgba(185, 184, 185, 1) 0%,
			rgba(194, 197, 226, 0.8995973389355743) 61%,
			rgba(229, 243, 252, 1) 100%
		);
		background: radial-gradient(
			circle,
			rgba(26, 14, 22, 1) 0%,
			rgba(185, 184, 185, 1) 0%,
			rgba(194, 197, 226, 0.8995973389355743) 61%,
			rgba(229, 243, 252, 1) 100%
		);
	}

	.flight-window {
		width: 180px;
		height: 240px;
		position: relative;
	}

	.window-frame {
		width: 100%;
		height: 100%;
		background: #d0d0d0;
		border-radius: 4.5rem;
		display: flex;
		justify-content: center;
		align-items: center;
		box-shadow:
			1px 0px 11px gray,
			0px 0px 0px 3px white,
			inset 1px 5px 6px 4px #00000059,
			inset -1px -5px 6px 4px rgba(255, 255, 255, 0.952),
			inset -1px -5px 6px 4px rgba(255, 255, 255, 0.952);
	}

	.window-glass {
		width: 85%;
		height: 85%;
		border-radius: 4.5rem;
		overflow: hidden;
		position: relative;
	}

	.window-image {
		width: 100%;
		height: 100%;
		background-size: cover;
		background-position: center;
	}

	.window-image-1 {
		background-image: url('../lib/assets/Tour-Eiffel.jpg');
	}

	.window-image-2 {
		background-image: url('../lib/assets/Building.jpg');
	}

	.window-image-3 {
		background-image: url('../lib/assets/Taj-Mahal.jpg');
	}

	.window-shield {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgb(200, 200, 200);
		transition: transform 0.5s ease-out;
		box-shadow:
			5px 1px 13px #80808000,
			1px -1px 0px 5px #ffffffe8,
			inset 1px 3px 13px 13px #00000026,
			inset -5px -10px 20px 4px rgb(255 255 255 / 55%),
			inset 4px 6px 7px 0px rgb(255 255 255 / 48%);
		border-radius: 3rem;
	}

	.window-shield::before {
		content: '';
		position: absolute;
		right: 50%;
		transform: translate(50%, 50%);
		bottom: 0;
		z-index: 1;
		width: 1rem;
		height: 0.3rem;
		background-color: black;
	}
</style>
