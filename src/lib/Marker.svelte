<script lang="ts">
	import { onMount, onDestroy, getContext, setContext, createEventDispatcher } from 'svelte';
	import L from 'leaflet';

	export let width: number;
	export let height: number;
	export let latLng: L.LatLngExpression;
	export let city: string;

	let marker: L.Marker | undefined;
	let markerElement: HTMLElement;

	const dispatch = createEventDispatcher();

	const onMarkerClick = (e: any) => {
		dispatch('click', city);
	};

	const { getMap }: { getMap: () => L.Map | undefined } = getContext('map');
	const map = getMap();

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
		}
	});

	onDestroy(() => {
		marker?.remove();
		marker = undefined;
	});
</script>

<div bind:this={markerElement} on:click={onMarkerClick} aria-role="button">
	{#if marker}
		<slot />
	{/if}
</div>
