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
		<h1 slot="title">
            Klimaat zolderkamer
		</h1>
		<h2>Temperatuur<br /><br /></h2>
		<Graph entity_id="sensor.zolderkamer_temperature" ,period="day" ,name="test" />

        <h2>Luchtvochtigheid<br /><br /></h2>
		<Graph entity_id="sensor.zolderkamer_humidity" , period="day" />
	</Modal>
{/if}