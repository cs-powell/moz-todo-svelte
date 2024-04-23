<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

	function sayClear() {
		dispatch('message', {
			text: 'Eraser'
		});
	}
</script>

<main>
    <button on:click = {sayClear} id="button-element">erase mode</button>
</main>

<style>
    #button-element {
        background-color: blue;
        color: yellow;
    }
</style>