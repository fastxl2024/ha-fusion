<script lang="ts">
	import { states } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import BrandLogo from '$lib/Images/Brands/Kleenex_logo.png';
	import GrassIcon from '$lib/Images/grass_icon.svg';
	import TreeIcon from '$lib/Images/tree_icon.svg';
	import WeedsIcon from '$lib/Images/weeds_icon.svg';
	import Radial from '$lib/Own_addons/Radial.svelte';

	export let isOpen: boolean;
	export let sel: any;

	let maxValue: number | undefined = undefined;

	let grassIcon: "$lib/Images/grass_icon.svg";
	// Reactive statement to get the entity based on selected entity id
	$: entity = $states[sel?.entity_id];

	// Function to format the date and time
	function formatDateTime(dateTimeString: string) {
		const options: Intl.DateTimeFormatOptions = {
			day: '2-digit',
			month: '2-digit',
			year: 'numeric',
			hour: '2-digit',
			minute: '2-digit',
			hour12: false
		};
		return new Intl.DateTimeFormat('nl-NL', options)
			.format(new Date(dateTimeString))
			.replace(',', ' om');
	}

	// Reactive statement to get the last updated time for the sensor
	$: lastUpdated = formatDateTime(
		$states?.['sensor.kleenex_pollen_radar_thuis_laatst_bijgewerkt'].state
	);
</script>

{#if isOpen}
	<Modal>
		<!-- Kleenex logo in title -->
		<img slot="title" src={BrandLogo} alt="Kleenex Logo" style="height: 40px;" />

		<h1>Pollenradar</h1>
		<br />
		<div class="container">
			<!-- Radial charts for different pollen types -->
			<Radial
				entity_id="sensor.kleenex_pollen_radar_thuis_gras"
				maxValue={342}
				name="Grassen"
				iconUrl={GrassIcon}
			></Radial>
			<Radial
				entity_id="sensor.kleenex_pollen_radar_thuis_kruiden"
				maxValue={267}
				name="Onkruid"
				iconUrl={WeedsIcon}
			></Radial>
			<Radial
				entity_id="sensor.kleenex_pollen_radar_thuis_bomen"
				maxValue={704}
				name="Bomen"
				iconUrl={TreeIcon}
			></Radial>
		</div>
		<div class="last_update">
			Laatste update: {lastUpdated} uur
		</div>
	</Modal>
{/if}

<style>
	/* Ensure the modal takes full screen and scales correctly
	.modal-content {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 100vw;  
		height: 100vh; 
		box-sizing: border-box;
		padding: 20px;
		overflow: hidden; 
	}
	*/
	.container {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 20px; /* Space between the radials */
		width: 100%;
		flex-wrap: wrap; /* Allow items to wrap on smaller screens */
	}

	@media (max-width: 768px) {
		.container {
			flex-direction: column;
		}
	}

	/* Style for the last update text */
	.last_update {
		margin-top: 20px;
		text-align: center;
		font-size: 16px;
	}
</style>
