<script lang="ts">
	import { states, lang } from '$lib/Stores';
	import Modal from '$lib/Modal/Index.svelte';
	import StateLogic from '$lib/Components/StateLogic.svelte';
	import ConfigButtons from '$lib/Modal/ConfigButtons.svelte';
	import { getName } from '$lib/Utils';
	import Bar from '$lib/Sidebar/Bar.svelte';
  import Ubiquiti_logo from '$lib/Images/ubiquitinetworks-edited.png'
  import UDM_SE_image from '$lib/Images/udm_se.png'
	import { ImageSource } from 'maplibre-gl';
	import Sensor from '$lib/Sidebar/Sensor.svelte';

	export let isOpen: boolean;
	export let sel: any;
  let status_color = '#0000FF';

	$: entity = $states['sensor.udm_se_info'];

</script>

{#if isOpen}
	<Modal>
		<h1 slot="title"><img src={Ubiquiti_logo} alt="test" style="max-width:120px; top:20px"></h1>
        <div class="port_container">
            <div class="Image"><img src={UDM_SE_image} alt="test" style="max-width:120px; top:20px"></div>
            <div class="Status">
              <div class="Uptime">
                <div class="Name">Uptime:</div>
                <div class="Value">{$states?.['sensor.udm_se_info']?.attributes.uptime}</div>
              </div>  
              <div class="CPU">
                <div class="Name">CPU Usage:</div>
                <div class="Value">{$states?.['sensor.udm_se_info']?.attributes.cpu} %</div>
              </div> 
              <div class="RAM">
                <div class="Name">RAM Usage:</div>
                <div class="Value">{$states?.['sensor.udm_se_info']?.attributes.memory} %</div>
              </div>  
              <div class="Speedtest">
                <div class="Name">Speedtest:</div>
                <div class="Value">{$states?.['sensor.udm_se_info']?.attributes.speedtest_down} Mbps / {$states?.['sensor.udm_se_info']?.attributes.speedtest_up} Mbps</div>
              </div>
            </div>
            <div class="Port1">
              <div class="Name">Port 1</div>
              <div class="Value"><StateLogic entity_id='sensor.udm_se_port_2_poe_power'/></div>
            </div>  
            <div class="Port2">
              <div class="Name">Port 2</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_2_poe_power'/></div>
            </div> 
            <div class="Port3">
              <div class="Name">Port 3</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_3_poe_power'/></div>
            </div> 
            <div class="Port4">
              <div class="Name">Port 4</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_4_poe_power'/></div>
            </div> 
            <div class="Port5">
              <div class="Name">Port 5</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_5_poe_power'/></div>
            </div> 
            <div class="Port6">
              <div class="Name">Port 6</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_6_poe_power'/></div>
            </div> 
            <div class="Port7">
              <div class="Name">Port 7</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_7_poe_power'/></div>
            </div> 
            <div class="Port8">
              <div class="Name">Port 8</div>
              <div class="Value">
              <StateLogic entity_id='sensor.udm_se_port_8_poe_power'/></div>
            </div> 
          </div>

		<ConfigButtons />
	</Modal>
{/if}



<style>
.port_container {  
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 0.2fr 0.2fr 0.2fr;
  gap: 0px 0px;
  grid-auto-flow: row;
  grid-template-areas:
    "Image Image Image Status Status Status Status Status"
    "Port1 Port2 Port3 Port4 Port5 Port6 Port7 Port8"
    ". . . . . . . .";
}

.Image { grid-area: Image; }
.Port1 {
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value"; 
  grid-area: Port1; 
}
.Name { grid-area: Name; }
.Value { grid-area: Value; }
.Port2 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value"; 
  grid-area: Port2; 
  }  
.Port3 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value"; 
  grid-area: Port3; 
  }
.Port4 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value"; 
  grid-area: Port4; 
  }
.Port5 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value"; 
  grid-area: Port5; 
  }
.Port6 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value";
  grid-area: Port6; 
  }
.Port7 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value";
  grid-area: Port7; 
  }
.Port8 { 
  display: grid; 
  grid-template-columns: 1fr 1fr; 
  grid-template-rows: 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Name"
    "Value Value";
  grid-area: Port8; 
  }
.Status { 
  display: grid; 
  grid-template-columns: 1fr 1fr 1fr; 
  grid-template-rows: 1fr 1fr 1fr 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Uptime Uptime Uptime"
    "CPU CPU CPU"
    "RAM RAM RAM"
    "Speedtest Speedtest Speedtest"; 
  grid-area: Status; 
  }
.Uptime { 
  display: grid; 
  grid-template-columns: 1fr 1fr 1fr; 
  grid-template-rows: 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Value Value";  
  grid-area: Uptime; 
  }
.CPU { 
  display: grid; 
  grid-template-columns: 1fr 1fr 1fr; 
  grid-template-rows: 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Value Value";
  grid-area: CPU;
 }
.RAM { 
  display: grid; 
  grid-template-columns: 1fr 1fr 1fr; 
  grid-template-rows: 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Value Value";
  grid-area: RAM; 
  }
.Speedtest { 
  display: grid; 
  grid-template-columns: 1fr 1fr 1fr; 
  grid-template-rows: 1fr; 
  gap: 0px 0px; 
  grid-template-areas: 
    "Name Value Value";  
  grid-area: Speedtest;
 }

</style>