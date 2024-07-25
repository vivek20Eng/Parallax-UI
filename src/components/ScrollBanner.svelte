<script lang="ts">
	import { onMount } from 'svelte';
	import birds from '../../src/lib/assets/birds.png';
	import cloud from '../../src/lib/assets/cloud.png';

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
				pin: true,
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

<div class="scroll-container w-full flex flex-col items-center">
	<div
		id="airplane-interior"
		class="airplane-interior w-full h-screen bg-gray-300 flex justify-center items-center overflow-hidden sticky top-0"
	>
	<img src={birds} data-speed="0.25" data-amplitude="30" data-offset-y="20" alt="bird" class="bg-blend-screen absolute top-32 left-[20%] sm:left-[40%] z-10 h-32" />
	<img src={cloud} data-speed="0.50" data-amplitude="15" data-offset-y="-10" alt="cloud" class="bg-blend-screen cloud absolute top-28 left-[10%] sm:left-[30%] z-10 h-32" />
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
			<p class="leding-4 text-lg text-white font-medium">
				Your journey is about to begin <br />
				Please Ensure Your Seatbelts are Fastened
			</p>
		</section>
	</div>
	
	<div class="content-section w-full max-w-4xl mt-8 p-4">
		<h1 class="text-3xl font-bold mb-4">Explore the World from Above</h1>
		<div class="grid grid-cols-3 gap-4">
			<div class="text-center">
				<img src="https://via.placeholder.com/150" alt="Cityscape" class="mx-auto mb-2 rounded" />
				<h3 class="font-semibold">Cityscapes</h3>
				<p>Marvel at urban landscapes from the sky</p>
			</div>
			<div class="text-center">
				<img src="https://via.placeholder.com/150" alt="Cloudscape" class="mx-auto mb-2 rounded" />
				<h3 class="font-semibold">Cloudscapes</h3>
				<p>Float through majestic cloud formations</p>
			</div>
			<div class="text-center">
				<img src="https://via.placeholder.com/150" alt="Sunset" class="mx-auto mb-2 rounded" />
				<h3 class="font-semibold">Sunsets</h3>
				<p>Witness breathtaking sunsets above the clouds</p>
			</div>
		</div>
	</div>
</div>


<style>
	.background-circle {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
	.airplane-interior {
		position: sticky;
		top: 0;
		/* background: linear-gradient(to bottom, #e0e0e0, #f0f0f0); */
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
		background-image: url('../lib//assets/Tour-Eiffel.jpg');
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
