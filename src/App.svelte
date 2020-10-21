<script>

	import { Popover, Button } from "@budibase/bbui"
	import NpsScore from "./Forms/NpsScore.svelte"
	import { onMount } from "svelte"

	let dropdown
	let button
	let mainElement

	const submitted = ev => {
		window.parent.postMessage({
			type: "submitted",
			data: ev.detail,
		}, "*")
	}

	onMount(() => {
		/*const observer = new ResizeObserver(entries => {
			window.parent.postMessage({
				type: "loaded",
				height: entries[0].contentRect.height,
				width: entries[0].contentRect.width,
			}, "*")
		})
		observer.observe(mainElement)*/
		window.parent.postMessage({
			type: "loaded",
			height: mainElement.getBoundingClientRect().height,
			width: mainElement.getBoundingClientRect().width,
		}, "*")
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