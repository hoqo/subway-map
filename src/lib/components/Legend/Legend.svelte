<script lang="ts">
	import LegendItem from './LegendItem.svelte';
	import type { iMapItem } from '$lib/interfaces';
	import { dniproRiver, subwayLines } from '$lib/components/Map/mocks';

	const legendItems: iMapItem[] = [
		dniproRiver,
		...subwayLines.map(({ name, colorCode }) => ({ name, colorCode }))
	];
</script>

<ul aria-label="Legend">
	{#each legendItems as item (item.name)}
		<LegendItem {item} />
	{/each}
</ul>

<style>
	ul {
		display: flex;
		gap: 16px;

		list-style-type: none;

		&:before {
			content: attr(aria-label);
			margin-bottom: 24px;
			font-size: 1.5em;
		}
	}
</style>
