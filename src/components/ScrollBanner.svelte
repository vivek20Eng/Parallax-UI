<script type="ts">
        // import gsap from "gsap";
        // import ScrollTrigger from "gsap/ScrollTrigger";

    //     gsap.to('.box', {
    //     scrollTrigger: '.box', 
    //     x: 500
    // });
    gsap.to("body", {backgroundColor: "red", duration: 3});
    </script>

    <div class="scroll-container w-full flex">
    <div class="flex relative justify-center items-center w-full h-full border-2 border-red-900">
	<div class="door-container flex w-6/12 h-full justify-between items-center">
		<div class="door door-left w-36 h-52 rounded-[3rem] relative">
			<div class="relative border-2 border-gray-600  window-image-1 rounded-[2rem] w-full h-full overflow-hidden z-10"></div>
            <div class="window-shield absolute w-full h-full bg-red-800/30 z-20 top-0 box"></div>
		</div>
		<div class="door door-center w-36 h-52 rounded-[3rem] ">
			<div class="window-image-2 w-full h-full overflow-hidden z-10 rounded-[2rem]"></div>
            <div class="window-shield absolute w-full h-full bg-red-800/30 z-20 top-0"></div>

		</div>
		<div class="door door-right w-36 h-52 rounded-[3rem]">
			<div class="window-image-3 w-full h-full overflow-hidden z-10 rounded-[2rem]"></div>
            <div class="window-shield absolute w-full h-full bg-red-800/30 z-20 top-0"></div>

		</div>
	</div>
    </div>
	<!-- <div class="content relative">
        Test
	</div> -->
</div>

<style>
    
	.scroll-container {
		height: 100vh;
		overflow-y: scroll;
		perspective: 1000px;
        z-index: -1;
	}

	/* .door-container {
		position: fixed;
		top: 0;
		left: 0;
		display: flex;
	} */

	.door {
		/* flex: 1;
		height: 100%; */
		background-color: #f0f0f0;
		transition: transform 0.5s ease-out;
		overflow: hidden;
		position: relative;
		z-index: 0;
        border: 15px solid rgb(233, 227, 227);
        box-shadow: 1px 0px 11px gray, 0px 0px 0px 3px white, inset 1px 5px 6px 4px #00000059,  inset -1px -5px 6px 4px rgba(255, 255, 255, 0.952),inset -1px -5px 6px 4px rgba(255, 255, 255, 0.952);
	}

	.window-image-1 {
		background-image: url('https://picsum.photos/200/300');
		border: 2px solid red;
	}
	.window-image-2 {
		background-image: url('https://picsum.photos/200/300');
        border: 2px solid blue;

	}
	.window-image-3 {
		background-image: url('https://picsum.photos/200/300');
        border: 2px solid green;

	}

	.content {
		height: 300vh;
		position: relative;
	}
</style>
