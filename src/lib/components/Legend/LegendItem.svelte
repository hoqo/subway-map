<script lang="ts">
	import type { iMapItem } from '$lib/interfaces';

	export let item: iMapItem;
</script>

<li>
	<span class="color-block" style="--color: {item.colorCode}"></span>
	<span class="name">{item.name}</span>
</li>

<style>
	li {
		display: inline-flex;
	}

	.color-block {
		background-color: var(--color);
		height: 24px;
		width: 24px;
		border-radius: 4px;
		margin-right: 16px;
	}
</style>
