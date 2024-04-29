<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import StateLogic from '$lib/Components/StateLogic.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import Bar from '$lib/Sidebar/Bar.svelte';
	import Proxmox_logo from '$lib/Images/Proxmox_logo.png';

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
					<div class="port_container">
						<div class="Image">
						</div>
						<div class="Status">
							<div class="Title_name">Name:</div>
							<div class="Title_name_Value">{udm_se.name}</div>
							<div class="Uptime">Uptime:</div>
							<div class="Uptime_Value">{udm_se.uptime}</div>
							<div class="Version">Firmware:</div>
							<div class="Version_Value">{udm_se.version}</div>
							<div class="CPU">CPU Usage:</div>
							<div class="CPU_Value">{udm_se.cpu} %</div>
							<div class="RAM">RAM Usage:</div>
							<div class="RAM_Value">{udm_se.memory} %</div>
							<div class="Speedtest">Speedtest:</div>
							<div class="Speedtest_Value">{udm_se.speedtest_down} Mbps / {udm_se.speedtest_up} Mbps
							</div>
							<div class="Speedtest_last_run">Last run:</div>
							<div class="Speedtest_last_run_Value">{udm_se.speedtest_run_date}</div>
						</div>
						<div
							class="Port1"
							style="background:{udm_se?.port1_connected ? 'green' : 'darkred'}"
							on:click={handleSpeedTest}
						>
							<div class="Name">Port 1</div>
							<div class="Value"><StateLogic entity_id="sensor.udm_se_port_2_poe_power" /></div>
						</div>
						<div class="Port2" style="background:{udm_se?.port2_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 2</div>
							<div class="Value">{udm_se.memory}</div>
						</div>
						<div class="Port3" style="background:{udm_se?.port3_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 3</div>
							<div class="Value">
								<StateLogic entity_id="sensor.udm_se_port_3_poe_power" />
							</div>
						</div>
						<div class="Port4" style="background:{udm_se?.port4_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 4</div>
							<div class="Value">
								<StateLogic entity_id="sensor.udm_se_port_4_poe_power" />
							</div>
						</div>
						<div class="Port5" style="background:{udm_se?.port4_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 5</div>
							<div class="Value">
								<StateLogic entity_id="sensor.udm_se_port_5_poe_power" />
							</div>
						</div>
						<div class="Port6" style="background:{udm_se?.port4_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 6</div>
							<div class="Value">
								<StateLogic entity_id="sensor.udm_se_port_6_poe_power" />
							</div>
						</div>
						<div class="Port7" style="background:{udm_se?.port4_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 7</div>
							<div class="Value">
								<StateLogic entity_id="sensor.udm_se_port_7_poe_power" />
							</div>
						</div>
						<div class="Port8" style="background:{udm_se?.port4_connected ? 'green' : 'darkred'}">
							<div class="Name">Port 8</div>
							<div class="Value">
								<StateLogic entity_id="sensor.udm_se_port_8_poe_power" />
							</div>
						</div>
					</div>
				</SwipeItem>
				<!--SWITCH TVKAST-->
				<SwipeItem>
				</SwipeItem>
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
	.Image {
		align-items: center;
		grid-area: Image;
	}

	.Name {
		grid-area: Name;
	}
	.Value {
		grid-area: Value;
	}
	.Port1 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port1;
	}
	.Port2 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port2;
	}
	.Port3 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port3;
	}
	.Port4 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port4;
	}
	.Port5 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port5;
	}
	.Port6 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port6;
	}
	.Port7 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port7;
	}
	.Port8 {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr;
		gap: 0px 0px;
		grid-template-areas:
			'Name Name'
			'Value Value';
		border-radius: 5px;
		text-align: center;
		grid-area: Port8;
	}
	.Status {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr;
		gap: 5px 0px;
		grid-template-areas:
			'Title_name Title_name Title_name_Value'
			'Uptime Uptime Uptime_Value'
			'Version Version Version_Value'
			'CPU CPU CPU_Value'
			'RAM RAM RAM_Value'
			'Speedtest Speedtest Speedtest_Value'
			'Speedtest_last_run Speedtest_last_run Speedtest_last_run_Value';
		grid-area: Status;
	}
	.Title_name {
		grid-area: Title_name;
	}
	.Title_name_Value {
		grid-area: Title_name_Value;
	}
	.Uptime {
		grid-area: Uptime;
	}
	.Uptime_Value {
		grid-area: Uptime_Value;
	}
	.Version {
		grid-area: Version;
	}
	.Version_Value {
		grid-area: Version_Value;
	}
	.CPU {
		grid-area: CPU;
	}
	.CPU_Value {
		grid-area: CPU_Value;
	}
	.RAM {
		grid-area: RAM;
	}
	.RAM_Value {
		grid-area: RAM_Value;
	}
	.Speedtest {
		grid-area: Speedtest;
	}
	.Speedtest_Value {
		grid-area: Speedtest_Value;
	}
	.Speedtest_last_run {
		grid-area: Speedtest_last_run;
	}
	.Speedtest_last_run_Value {
		grid-area: Speedtest_last_run_Value;
	}
</style>
