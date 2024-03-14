<script lang="ts">
	import '../app.css';
	import type { LatLng, LatLngExpression } from 'leaflet';
	import Leaflet from '$lib/Leaflet.svelte';
	import Marker from '$lib/Marker.svelte';
	import Popup from '$lib/Popup.svelte';

	const initialView: LatLngExpression = [40.4165, -3.70256];

	const contenidoPopupDinamico = {
		Madrid: 'Bienvenido a Madrid!',
		Barcelona: 'Bienvenido a Barcelona',
		Palma: 'Bienvenido a Palma',
		London: 'Welcome to London',
		Amsterdam: 'Welcome to Amsterdam',
		'New York': 'Welcome to New York',
		Roma: 'Welcome to Roma',
		Paris: 'Welcome to Paris',
		'Los Angeles': 'Welcome to Los Angeles',
		Cairo: 'Welcome to Cairo',
		Berlin: 'Welcome to Berlin',
		Sydney: 'Welcome to Sydney',
		Atlanta: 'Welcome to Atlanta'
	};

	let markerLocations = [
		['Madrid', [40.4165, -3.70256]],
		['Barcelona', [41.3879, 2.16992]],
		['Palma', [39.5519, 2.7388]],
		['London', [51.509865, -0.118092]],
		['Amsterdam', [52.3676, 4.9041]],
		['New York', [40.6413, -73.7781]],
		['Roma', [41.8005, 12.2558]],
		['Paris', [48.8566, 2.3522]],
		['Los Angeles', [34.0522, -118.2437]],
		['Cairo', [30.0444, 31.2357]],
		['Berlin', [52.52, 13.405]],
		['Sydney', [-33.8688, 151.2093]],
		['Atlanta', [33.749, -84.388]]
	];

	// const randomCoords = () => {
	// 	const lat = Math.random() * 180 - 90;
	// 	const lng = Math.random() * 360 - 180;

	// 	const latlng = [lat, lng] as LatLngExpression;
	// 	return latlng;
	// };

	// const addMarker = () => {
	// 	console.log('Adding marker');
	// 	markerLocations.push(randomCoords());
	// 	markerLocations = markerLocations;
	// };

	// setInterval(addMarker, 3000);

	let contenidoDelPopup = 'lorem ipsum dolor sit amet, consectetur adipiscing elit.';
	// setInterval(() => (contenidoDelPopup += " " + Date.now().toString()), 3000);

	const onMarkerClick = (e: any) => {
		console.log('Marker clicked', e.detail);
		// fetch con e.detail
		contenidoDelPopup = contenidoPopupDinamico[e.detail];
	};
</script>

<div class="w-full h-screen">
	<Leaflet view={initialView} zoom={5}>
		{#each markerLocations as [city, latLng]}
			<Marker {latLng} {city} width={40} height={40} on:click={onMarkerClick}>
				<div>🧡 {city}</div>
				<Popup>
					{contenidoDelPopup}
				</Popup>
			</Marker>
		{/each}
	</Leaflet>
</div>
