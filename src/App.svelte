<script>

	import { createEventDispatcher } from 'svelte';

	import Canvas from "./Canvas.svelte";
	
	const dispatch = createEventDispatcher();

	const clearDispatch = dispatch('message', {
			text: 'Clear'
		});

	
	const backgroundColor = Canvas.backgroundColor;
	let color = Canvas.color;
	

  const  HandleButtonClick = event => {
    context.clearRect(0,0,canvas.width,canvas.height);
  };

  
  

 

</script>



<main>
	<h1>Draw a Turtle!</h1>

<div id="main-box">
	<div id="canvas-box">
		<Canvas {color} {backgroundColor} />
	</div>

	<div id="control-box">
		
    	
		
	</div>

</div>
</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	/* #canvas-element {
		background-color:black;
	} */

	#main-box {
		justify-content: space-evenly;
	}

	div{
		display:block; 
	}
</style>