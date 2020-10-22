<script>

	import { Popover, Button } from "@budibase/bbui"
	import NpsScore from "./Forms/NpsScore.svelte"
	import { afterUpdate } from "svelte"

	let dropdown
	let button
	let mainElement

	const submitted = ev => {
		window.parent.postMessage({
			type: "submitted",
			data: ev.detail,
		}, "*")
	}

	const sendResizeMessage = (height, width) => {
		window.parent.postMessage({
			type: "loaded",
			height: height,
			width: width,
		}, "*")
	}

	afterUpdate(() => {
		sendResizeMessage(mainElement.getBoundingClientRect().height, mainElement.getBoundingClientRect().width)
	})

</script>

<main bind:this={mainElement}>
	<NpsScore on:submitted={submitted}/>
</main>

<style>
	main {
		text-align: center;
		display: inline;
	}

</style>