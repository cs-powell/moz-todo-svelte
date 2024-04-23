<script>
    import Clear from "./Clear.svelte";
	export let name;

	import { createEventDispatcher } from 'svelte';
    import Eraser from "./eraser.svelte";
	import Canvas from "./Canvas.svelte";

	const dispatch = createEventDispatcher();

	const clearDispatch = dispatch('message', {
			text: 'Clear'
		});

	function handleClearMessage(event) {
			alert("Screen Cleared");
			context.clearRect(0,0,canvas.width,canvas.height);
	}

	const backgroundColor = Canvas.backgroundColor;
	let color = Canvas.color;


	//Canvas Handling Events
	

  const  HandleButtonClick = event => {
    context.clearRect(0,0,canvas.width,canvas.height);
  };

  const  HandleEraseClick = event => {
    if(eraser == true) {
      setEraser(false);
      setColor(picker.value);
    } else {
      setEraser(true);
      setColor("white");
    }
    
  };

  const  HandleSlider = event => {
    setLineWidth(slider.value);
    // alert(lineWidth);
  };

  const  HandleColor = event => {
    setColor(picker.value);
  };

</script>



<main>
	<h1>Hello {name}!</h1>

<div id="main-box">
	<div id="canvas-box">
		<Canvas {color} {backgroundColor} />
	</div>

	<div id="control-box">
		<input id="color-picker" type = "color">
    	<input id="width-slider" type = "range" min="1" max="10">
		<Clear on:message = {handleClearMessage} />
	</div>

</div>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps. </p>
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

	#canvas-element {
		background-color:black;
	}

	#main-box {
		justify-content: space-evenly;
	}

	div{
		display:block; 
	}
</style>