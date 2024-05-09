<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import GoogleTv_logo from '$lib/Images/Google_TV_logo.png';

	export let isOpen: boolean;
	export let sel: any;

	let attributes: any;
	let interval: ReturnType<typeof setInterval>;
	let tick = Date.now();
	let isDragging = false;
	let debouncePosition = false;
	let debounceTimeout: ReturnType<typeof setTimeout>;
	let rangeValue = 0;
	let pendingRequest = false;
	let nextPosition: number | undefined = undefined;
	let currentSliderValue = 0;

	$: entity = $states[sel?.entity_id];
	$: entity_id = sel?.entity_id;
	$: attributes = entity?.attributes;
	$: playing = entity?.state === 'playing';
	$: updated_at = new Date(attributes?.media_position_updated_at).getTime();
	$: diff = (tick - updated_at) / 1000;
	$: position = attributes?.media_position + (playing ? diff : 0);
//    $: zolderkamer_entity = media_player.google_tv_android_tv_zolderkamer;

//	const swipeConfig = {
//		autoplay: false,
//		delay: 2000,
//		showIndicators: true,
//		transitionDuration: 1000,
//		defaultIndex: 0
//	};
//
//	const DEBOUNCE_INTERVAL = 2500;
//
//	onMount(() => {
//		if (playing) {
//			interval = setInterval(() => {
//				tick = Date.now();
//			}, 1000);
//		} else {
//			tick = Date.now();
//		}
//	});
//
//	$: rangeValue =
//		!debouncePosition && !isDragging
//			? Math.min(position || 0, attributes?.media_duration || 0)
//			: rangeValue;
//
//	onMount(() => {
//		// selectedSource = attributes?.source_list?.includes(attributes?.app_name)
//		// 	? attributes?.app_name
//		// 	: '';
//	});
//
//	onDestroy(() => {
//		clearInterval(interval);
//	});
//
//	async function handleChange(value: number) {
//		currentSliderValue = value;
//		debouncePosition = true;
//		clearTimeout(debounceTimeout);
//		debounceTimeout = setTimeout(() => {
//			debouncePosition = false;
//			rangeValue = position || 0;
//		}, DEBOUNCE_INTERVAL);
//		if (pendingRequest) {
//			if (nextPosition !== value) {
//				nextPosition = value;
//			}
//		} else {
//			pendingRequest = true;
//			try {
//				await callService($connection, 'media_player', 'media_seek', {
//					entity_id: entity?.entity_id,
//					seek_position: value
//				});
//			} catch (error) {
//				console.error('Failed to change position:', error);
//			}
//			pendingRequest = false;
//			if (nextPosition !== undefined && nextPosition !== value) {
//				const position = nextPosition;
//				nextPosition = undefined;
//				handleChange(position);
//			}
//		}
//	}
//
//	function handleClick(service: string) {
//		callService($connection, 'media_player', service, {
//			entity_id: entity_id
//		});
//	}

	//	function handleClickfavorite(favorite: string) {
	//		callService($connection, 'media_player', 'play_media', {
	//			entity_id: (sel, entity_id),
	//			media_content_type: 'favorite_item_id',
	//			media_content_id: favorite
	//		});
	//	}

//	function convertToHMS(seconds: number) {
//		if (seconds) {
//			const h = Math.floor(seconds / 3600);
//			const m = Math.floor((seconds % 3600) / 60);
//			const s = Math.floor(seconds % 60);
//			const hDisplay = h > 0 ? h + ':' : '';
//			const mDisplay = m < 10 ? '0' + m + ':' : m + ':';
//			const sDisplay = s < 10 ? '0' + s : s;
//			return hDisplay + mDisplay + sDisplay;
//		}
//	}
</script>

{#if isOpen}
	<Modal>
        {#if entity_id = 'media_player.zolderkamer_google_tv_2'}
            <h1><img src={GoogleTv_logo} alt="test" style="max-width:120px; top:20px" /></h1>
    		<h2>
    			{#if attributes?.media_artist}
    				{attributes?.media_artist}
    			{/if}

    			{#if attributes?.media_artist && attributes?.media_title}
    				-
    			{/if}

    			{#if attributes?.media_title && !attributes?.media_series_title}
    				{attributes?.media_title}
    			{/if}
                {#if attributes?.app_id}
                    {$states?.['media_player.google_tv_android_tv_zolderkamer'].attributes?.app_name}
                {/if}                 
    			{#if attributes?.media_album_name}
    				<br />Album: {attributes?.media_album_name}
    			{/if}
    		</h2>
            {#if attributes?.media_artist || attributes?.media_title}
                {#if attributes.media_title === 'Line-in'}
                    <img src={Sonos_line_in_icon} />
                {/if}
                {#if attributes?.entity_picture}
                    <img src={attributes?.entity_picture} alt={attributes?.media_title} />
            {/if}
        {/if}            
        {:else if entity_id = 'media_player.chromecast_slaapkamer'}
            <h1>test</h1>
        {/if}
	</Modal>
{/if}
