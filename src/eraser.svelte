<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

	function sayErase() {
		dispatch('message', {
			text: 'Eraser'
		});
	}
</script>

<main>
    <button on:click = {sayErase} id="button-element">erase mode</button>
</main>

<style>
    #button-element {
        background-color: blue;
        color: yellow;
    }
</style>