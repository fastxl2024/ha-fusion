<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import StateLogic from '$lib/Components/StateLogic.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import Bar from '$lib/Sidebar/Bar.svelte';
	import Proxmox_logo from '$lib/Images/Proxmox_logo.png';
	import { useLocation } from "svelte-routing"

	import { ImageSource } from 'maplibre-gl';
	import Sensor from '$lib/Sidebar/Sensor.svelte';
	import { redirect } from '@sveltejs/kit';
	import { Swipe, SwipeItem } from 'svelte-swipe';
	import { greatestIndex } from 'd3-array';

	$: udm_se = $states['sensor.udm_se_info'].attributes;
	const swipeConfig = {
		autoplay: false,
		delay: 2000,
		showIndicators: true,
		transitionDuration: 1000,
		defaultIndex: 0
	};

	//  export let sel: any;
	export let isOpen: boolean;
	//	export let sel: any;
	//  export let color: any;
</script>

{#if isOpen}
	<Modal>
		<h1 slot="title"><img src={Proxmox_logo} alt="test" style="max-width:120px; top:20px" /></h1>
		<div class="swipe-holder">
			<Swipe {...swipeConfig}>
				<SwipeItem>
					<Bar entity_id="sensor.node_proxmox_cpu_used" />
					<Bar entity_id="sensor.node_proxmox_memory_used_percentage" />
					<StateLogic entity_id="sensor.disk_proxmox_dev_nvme0n1_temperature" />
				</SwipeItem>
				<SwipeItem></SwipeItem>
			</Swipe>
		</div>
		<ConfigButtons />
	</Modal>
{/if}

<style>
	.swipe-holder {
		height: 50vh;
		width: 95%;
	}
	img {
		max-width: 120%;
		height: auto;
	}

	@media (max-width: 599px) {
		.port_container {
			display: grid;
			grid-template-columns: 1fr 1fr 1fr 1fr;
			grid-template-rows: repeat(5, 0.2fr);
			gap: 0px 0px;
			grid-auto-flow: row;
			grid-template-areas:
				'Image Image'
				'Status Status'
				'. . '
				'Port1 Port2 Port3 Port4'
				'Port5 Port6 Port7 Port8';
		}
		.Status {
			display: grid;
			grid-template-columns: 1fr 1fr;
			grid-template-rows: auto 1fr 1fr 1fr 1fr 1fr 1fr;
			gap: 2px 0px;
			grid-template-areas:
				'Title_name Title_name Title_name_Value'
				'Uptime Uptime Uptime_Value'
				'Version Version Version_Value'
				'CPU CPU CPU_Value'
				'RAM RAM RAM_Value'
				'Speedtest Speedtest Speedtest_Value';
			grid-area: Status;
		}
	}
	@media (min-width: 600px) {
		.port_container {
			display: grid;
			grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
			grid-template-rows: 0.2fr 0.2fr 0.2fr 0.2fr;
			gap: 5px 5px;
			grid-auto-flow: row;
			grid-template-areas:
				'Image Image Image Status Status Status Status Status'
				'. . . . . . . .'
				'Port1 Port2 Port3 Port4 Port5 Port6 Port7 Port8';
		}
	}
</style>
