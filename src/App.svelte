{#if num_slides == 0}
	<center>
		<div class="issue">
		<h1>Mi spiace ma non ci sono slide disponibili!!</h1>
		<h2>imposta il numero di slide con la variabile NUM_SLIDES=n</h2>
		<h2>ricordati di posizionare le slide nella directory public\slides</h2>
		</div>
	</center>
{:else}
	<Carousel bind:this={carousel} on:change={slideChange} perPage=1>
		<span class="control" slot="left-control">
	    	<ChevronLeftIcon />
	  	</span>
	  
	  	{#each slides as {},i}
			<Slide num={i+1} />
		{/each}

	   <span class="control" slot="right-control">
	    <ChevronRightIcon />
	  </span>
	</Carousel>
{/if}
<svelte:window on:keydown={handleKeydown}/>

<script>
	import Carousel from '@beyonk/svelte-carousel'
	import { ChevronLeftIcon, ChevronRightIcon } from 'svelte-feather-icons'
	import Slide from './Slide.svelte'
	
	let carousel;
	let num_slides = process.env.numSlides ? 0 : NUMSLIDES;
        console.log(num_slides);
	let slides = Array(num_slides);
	let currSlide = 1;

	function handleKeydown(event) {
		let keyCode = event.keyCode;
		if (keyCode == 37 && currSlide > 1)
			carousel.left();
		else if (keyCode == 39 && currSlide < num_slides)
			carousel.right();
	}

	function slideChange(event) {
		currSlide = event.detail.currentSlide + 1; 
	}
</script>

<style>
	.control :global(svg) {
		width: 100%;
		height: 100%;
		color: black;
		border: 3px solid black;
		border-radius: 32px;
	}

.issue {
	width: 50%;
	margin-top: 10rem;
	-moz-border-radius: 5px;
	-webkit-border-radius: 5px;
	border-radius: 5px;
	color: #ffffff;
	background-color: #3498db;
	font-family: verdana, 'open sans', sans-serif;
	font-size: 12pt;
	margin-bottom: 25px;
	padding: 10px 14px 10px 44px;
	position: relative;
	box-shadow: 15px 15px 15px #999;
}
</style>
