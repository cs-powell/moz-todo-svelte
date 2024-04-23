<script>


import { onMount } from 'svelte'
import Eraser from "./eraser.svelte";

    export let width = 800
	export let height = 600
	export let color = '#333'
	export let backgroundColor = '#343'
    export let lineWidth = 5;
    export let eraser = false;

    let context;
    let canvas;
    let isDragging;

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




</script>


    <canvas 
    {width}
    {height}
    id="canvas-element" width = "800" height = "600"></canvas>
