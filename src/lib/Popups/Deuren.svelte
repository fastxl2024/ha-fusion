<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import StateLogic from '$lib/Components/StateLogic.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import Bar from '$lib/Sidebar/Bar.svelte';

	export let isOpen: boolean;
	export let sel: any;

	$: entity = $states[sel?.entity_id];
</script>

{#if isOpen}
	<Modal>
		<h1 slot="title">{getName(sel, entity)}</h1>
		<br />
		<div class="container">
			<div class="Entiteit1">Voordeur</div>
			<div class="Entiteit2">Achterdeur</div>
			<div class="Status1"><StateLogic entity_id={sel?.entity_id} selected={sel} /></div>
			<div class="Status2"><StateLogic entity_id="binary_sensor.achterdeur_contact" /></div>
			<div class="Laatst-geopend1">
				{$states?.['binary_sensor.voordeur_contact']?.attributes.last_seen
					.replace('T', ' ')
					.split('.')[0]}
			</div>
			<div class="Laatst-geopend2">
				{$states?.['binary_sensor.achterdeur_contact']?.attributes.last_seen
					.replace('T', ' ')
					.split('.')[0]}
			</div>
		</div>
		<ConfigButtons />
	</Modal>
{/if}

<style>
	.container {
		display: grid;
		grid-template-columns: 0.6fr 0.6fr 1fr;
		grid-template-rows: 1fr 1fr;
		grid-auto-columns: 1fr;
		gap: 10px 0px;
		grid-auto-flow: row;
		grid-template-areas:
			'Entiteit1 Status1 Laatst-geopend1'
			'Entiteit2 Status2 Laatst-geopend2';
	}

	.Entiteit1 {
		grid-area: Entiteit1;
	}
	.Entiteit2 {
		grid-area: Entiteit2;
	}
	.Status1 {
		grid-area: Status1;
	}
	.Status2 {
		grid-area: Status2;
	}
	.Laatst-geopend1 {
		grid-area: Laatst-geopend1;
	}
	.Laatst-geopend2 {
		grid-area: Laatst-geopend2;
	}
</style>
