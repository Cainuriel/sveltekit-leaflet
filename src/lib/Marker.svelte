<script lang="ts">
	import { onMount, onDestroy, getContext, setContext } from 'svelte';
	import L from 'leaflet';
	export let width: number;
	export let height: number;
	export let latLng: L.LatLngExpression;
	export let name: string;
	export let action: string;
	let marker: L.Marker | undefined;
	let markerElement: HTMLElement;

	const { getMap }: { getMap: () => L.Map | undefined } = getContext('map');
	const map = getMap();

	function handleClick() {
		console.log(action, "en ", name);
	}

	setContext('layer', {
		// L.Marker inherits from L.Layer
		getLayer: () => marker
	});

	onMount(() => {
		if (map) {
			let icon = L.divIcon({
				html: markerElement,
				className: 'map-marker',
				iconSize: L.point(width, height)
			});
			marker = L.marker(latLng, { icon }).addTo(map);
			marker.on('click', handleClick);
		}
	});

	onDestroy(() => {
		marker?.remove();
		marker = undefined;
	});
</script>



<div class="map-marker" bind:this={markerElement}>
	{#if marker}
		<slot />
	{/if}
</div>

<style>
	.map-marker {
		transform: translate(-50%, -50%);
	}
</style>