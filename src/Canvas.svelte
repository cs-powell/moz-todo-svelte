<script>


import { onMount } from 'svelte'
    import Eraser from "./eraser.svelte";
    import Clear from "./Clear.svelte";

    export let width = 800
	export let height = 600
	export let color = '#fff'
	let backgroundColor = '#343'
    export let lineWidth = 5;
    export let eraser = false;

    let context;
    let canvas;
    let isDragging;

    function handleClearMessage(event) {
			alert("Screen Cleared");
			context.clearRect(0,0,canvas.width,canvas.height);
	}

 const HandleColor = event => {
    alert("Handling Color");
    context.strokeStyle = color;
  };

    function setIsDragging(input){
        isDragging = input;
    }
    

    function setEraser(input){
        eraser = input;
    }
    

    function mount() {
        context = canvas.getContext("2d");
        context.lineWidth = lineWidth;
    }

    onMount(mount);

    $: if(context){
        context.strokeStyle = color; 
    }

    const HandleMouseDown = event => {
      setIsDragging(true);
      console.log("Mouse is moving over the canvas");
      context.beginPath();
      context.moveTo(event.offsetX, event.offsetY);
  };

  const HandleMouseMove = event => {
      if(isDragging && !eraser) {
        console.log("We should be dragging and drawing");
        // context.fillRect(event.offsetX, event.offsetY, 3,3);
        context.lineWidth = lineWidth;
        context.strokeStyle = color;
        context.lineTo(event.offsetX, event.offsetY);
        context.stroke(); 
    } else if(isDragging && eraser) {
      context.lineWidth = lineWidth;
      context.strokeStyle = color;
      context.lineTo(event.offsetX, event.offsetY);
      context.stroke();
        console.log("Mouse is moving over the canvas, but we erase");
    }
  };

  const HandleMouseUp = event => {
    // alert("made it to mouse up");
    setIsDragging(false);
  };


  const  HandleEraseClick = event => {
    if(eraser == true) {
      setEraser(false);
      setColor(picker.value);
    } else {
        alert("eraser on");
      setEraser(true);
      color = "black";
    }
  };

  const  HandleSlider = event => {
    lineWidth = lineWidth;
    // alert(lineWidth);
  };

</script>


    <canvas 
    bind:this={canvas}
    {width}
    {height}
    id="canvas-element" 
    on:mousedown={HandleMouseDown}
    on:mousemove={HandleMouseMove}
    on:mouseup={HandleMouseUp}
    style="background: black;"
    ></canvas>
    <div id = "control1">
        <input bind:value = {color} on:change = {HandleColor} id= "color-picker" type = "color"/>
        <Clear on:message = {handleClearMessage} />
        <Eraser on:message = {HandleEraseClick} /> 
        <input bind:value = {lineWidth} on:change = {HandleSlider} id="width-slider" type = "range" min="1" max="10">
    </div>
    

    <style>
        #control1 {
            justify-content: left;
        }
    </style>