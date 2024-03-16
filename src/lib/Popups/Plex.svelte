<script lang="ts">
	import Modal from '$lib/Modal/Index.svelte';
	import { states } from '$lib/Stores';
	import { getName } from '$lib/Utils';
	import { Swipe, SwipeItem } from "svelte-swipe";

    const swipeConfig = {
      autoplay: false,
      delay: 2000,
      showIndicators: true,
      transitionDuration: 1000,
      defaultIndex: 0,
    };

	export let isOpen: boolean;
	export let sel: any;

	$: entity = $states[sel?.entity_id];
</script>

{#if isOpen}
	<Modal>
        <h1 slot="title">{getName(sel, entity)}</h1>
        <div class="swipe-holder">
            <Swipe {...swipeConfig}>
              <SwipeItem>
                <div class="container">
                  <div class="Media">
                    <img src={$states?.['sensor.plex_recently_added']?.attributes.data[1].poster} alt="episode_picture">
                  </div>                
                  <div class="Info">
                    <div class="Title">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[1].title}
                    </div>
                    <div class="Episode">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[1].number} - {$states?.['sensor.plex_recently_added']?.attributes.data[1].episode}
                    </div>
                    <div class="Air-date">
                      Uitgezonden: {$states?.['sensor.plex_recently_added']?.attributes.data[1].aired}
                    </div>
                  </div>
                </div>                
              </SwipeItem>        
              <SwipeItem>
                <div class="container">
                  <div class="Media">
                    <img src={$states?.['sensor.plex_recently_added']?.attributes.data[2].poster} alt="episode_picture">
                  </div>                
                  <div class="Info">
                    <div class="Title">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[2].title}
                    </div>
                    <div class="Episode">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[2].number} - {$states?.['sensor.plex_recently_added']?.attributes.data[2].episode}
                    </div>
                    <div class="Air-date">
                      Uitgezonden: {$states?.['sensor.plex_recently_added']?.attributes.data[2].aired}
                    </div>
                  </div>
                </div>                
              </SwipeItem>
              <SwipeItem>
                <div class="container">
                  <div class="Media">
                    <img src={$states?.['sensor.plex_recently_added']?.attributes.data[3].poster} alt="episode_picture">
                  </div>                
                  <div class="Info">
                    <div class="Title">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[3].title}
                    </div>
                    <div class="Episode">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[3].number} - {$states?.['sensor.plex_recently_added']?.attributes.data[3].episode}
                    </div>
                    <div class="Air-date">
                      Uitgezonden: {$states?.['sensor.plex_recently_added']?.attributes.data[3].aired}
                    </div>
                  </div>
                </div>                
              </SwipeItem>
              <SwipeItem>
                <div class="container">
                  <div class="Media">
                    <img src={$states?.['sensor.plex_recently_added']?.attributes.data[4].poster} alt="episode_picture">
                  </div>                
                  <div class="Info">
                    <div class="Title">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[4].title}
                    </div>
                    <div class="Episode">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[4].number} - {$states?.['sensor.plex_recently_added']?.attributes.data[4].episode}
                    </div>
                    <div class="Air-date">
                      Uitgezonden: {$states?.['sensor.plex_recently_added']?.attributes.data[4].aired}
                    </div>
                  </div>
                </div>                
              </SwipeItem>
              <SwipeItem>
                <div class="container">
                  <div class="Media">
                    <img src={$states?.['sensor.plex_recently_added']?.attributes.data[5].poster} alt="episode_picture">
                  </div>                
                  <div class="Info">
                    <div class="Title">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[5].title}
                    </div>
                    <div class="Episode">
                      {$states?.['sensor.plex_recently_added']?.attributes.data[5].number} - {$states?.['sensor.plex_recently_added']?.attributes.data[5].episode}
                    </div>
                    <div class="Air-date">
                      Uitgezonden: {$states?.['sensor.plex_recently_added']?.attributes.data[5].aired}
                    </div>
                  </div>
                </div>                
              </SwipeItem>                                          
        </Swipe>
      </div>                            
	</Modal>
{/if}        

<style>
    .swipe-holder{
      height: 40vh;
      width: 95%;
    }
    img{
      max-width: 120%;
      height: auto;
    }

    .container {
      display: grid; 
      grid-template-columns: 1fr 1fr 1fr; 
      grid-template-rows: 1fr 1fr 1fr; 
      gap: 0px 0px; 
      grid-template-areas: 
        "Media Media Info"
        "Media Media Info"
        "Media Media Info"; 
    }
    .Media { grid-area: Media; }
    .Info {
      display: grid; 
      grid-template-columns: 1fr 1fr 1fr; 
      grid-template-rows: 1fr 1fr 1fr; 
      gap: 0px 0px; 
      grid-template-areas: 
        "Title Title Title"
        "Episode Episode Episode"
        "Air-date Air-date Air-date"; 
      grid-area: Info; 
    }
    .Title { grid-area: Title; }
    .Episode { grid-area: Episode; }
    .Air-date { grid-area: Air-date; }    
    
  </style>