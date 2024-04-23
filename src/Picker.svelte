<script>

// export var pickerColor2;

    import { createEventDispatcher } from 'svelte';

    let pickerColor1;

    export {pickerColor1 as pickerColor2};

    const dispatch = createEventDispatcher();

	function sayPick() {
		dispatch('message', {
			text: 'Pick'
		});

	}
</script>

<main>
    <input bind:value = {pickerColor1} on:change = {sayPick} id= "color-picker" type = "color"/>
</main>

<style>

</style>