<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import StateLogic from '$lib/Components/StateLogic.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import Bar from '$lib/Sidebar/Bar.svelte';
	import Graph from '$lib/Sidebar/Graph.svelte';

	export let isOpen: boolean;
	export let sel: any;

	$: entity = $states[sel?.entity_id];
</script>

{#if isOpen}
	<Modal>
		<h1 slot="title"><img src="https://www.solaredge.com/nl/sites/nl/files/SolarEdge_logo_header_new_0.svg" alt="test" style="max-width:120px; top:20px"></h1>
		<Bar entity_id='sensor.solaredge_temp_sink' /><br>
		<h2>Opgewekt:<br><br></h2>
		Momenteel: <StateLogic entity_id='sensor.solaredge_ac_power' /> <br><br>
		Vandaag: <StateLogic entity_id='sensor.solaredge_energy_today'/> <br><br>
		Deze maand: <StateLogic entity_id='sensor.solaredge_energy_this_month'/> <br><br>
		Dit jaar: <StateLogic entity_id='sensor.solaredge_energy_this_year'/> <br><br>
		Aantal bomen geplant: <StateLogic entity_id='sensor.solaradge_bomen_geplant' />
<!--	<Graph entity_id='sensor.nintendo_switch_power', period='day'/>-->
	</Modal>
{/if}

<style>

</style>