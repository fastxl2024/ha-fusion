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
		<h1 slot="title">{getName(sel, entity)}</h1>

		<Bar entity_id='sensor.solaredge_heatsink_temp' /><br>
		Wekt nu op <StateLogic entity_id={sel?.entity_id} selected={sel} /> <br><br>
		Aantal bomen geplant <StateLogic entity_id='sensor.solaradge_bomen_geplant' />
		<Graph entity_id='sensor.solaredge_heatsink_temp' period='day' />
		<ConfigButtons />
	</Modal>
{/if}
