<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

	function sayClear() {
		dispatch('message', {
			text: 'Clear'
		});
	}
</script>

<main>
    <button on:click = {sayClear} id="button-element">Clear All</button>
</main>

<style>
    #button-element {
        background-color: blue;
        color: yellow;
    }
</style>