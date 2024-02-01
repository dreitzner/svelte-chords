<script lang="ts">
	import { draggable } from '@neodrag/svelte';
	import type { DragOptions } from '@neodrag/svelte';
	export let textLine: string;
	export let chordsSorted: {
		chord: string;
		position: number;
	}[];
	// TODO: emit change or pass in stores

	let options: DragOptions = {
		axis: 'x',
		bounds: 'parent', // TODO: calculate left and right for each chord
	};
</script>

<div class="relative pt-4">
	{#each chordsSorted as { chord, position }}
		<div use:draggable={options} class="chord absolute top-0 font-mono font-bold" style:--position={position}>
			{chord}
		</div>
	{/each}
	<textarea
		class="resize-none overflow-hidden py-1 font-mono"
		name="textLine"
		rows="1"
		cols="80"
		maxlength="80"
		bind:value={textLine}
	></textarea>
</div>

<style>
	.chord {
		left: calc(var(--position) * 1ch);
	}
</style>
