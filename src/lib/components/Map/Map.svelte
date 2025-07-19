<script lang="ts">
	// import River from '$lib/components/River/River.svelte';
	import { subwayLines } from './mocks';
	import { curveCatmullRom, line } from 'd3';
	import type { iSubwayStation } from '$lib/interfaces';

	const lineGenerator = line().curve(curveCatmullRom.alpha(1));

	// filter through all nodes and get only those that have a name -> hence a station
	// TODO: consider having styling nodes and stations separately
	/** @param {import('$lib/interfaces').iSubwayStation[]} nodes */
	const getSwStations = (nodes: iSubwayStation[]) => nodes.filter(({ name }) => !!name);

	/** @param {import('$lib/interfaces').iSubwayStation[]} nodes */
	const getPathD = (nodes: iSubwayStation[]) => nodes.map(({ point }) => Object.values(point));
</script>

<!--<River />-->

<svg id="map" height="747" width="100%" viewBox="0 0 3500 3500">
	{#each subwayLines as { nodes, colorCode, name } (name)}
		<g fill="none">
			<path d={lineGenerator(getPathD(nodes))} stroke={colorCode} stroke-width="30" />

			{#each getSwStations(nodes) as { name, point: { x, y } } (name)}
				<circle cx={x} cy={y} fill={colorCode} r="50" />
				<text>{name}</text>
			{/each}
		</g>
	{/each}
</svg>

<style>
	#map {
		z-index: 1;
	}
</style>
