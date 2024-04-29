<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import StateLogic from '$lib/Components/StateLogic.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import Bar from '$lib/Sidebar/Bar.svelte';
	import Test from '$lib/Modal/DeviceTrackerModal.svelte';

	export let isOpen: boolean;
	export let sel: any;

	$: entity = $states[sel?.entity_id];
</script>

{#if isOpen}
	<Modal>
		<h1 slot="title">{getName(sel, entity)}</h1>

		<h2>{$lang('state')}</h2>
		<Bar entity_id={sel?.entity_id} selected={sel} />
		<StateLogic entity_id={sel?.entity_id} selected={sel} />
		<Test />
		<ConfigButtons />
	</Modal>
{/if}
