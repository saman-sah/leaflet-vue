<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- Search / Result -->
    <div class="flex justify-center relative px-4 pt-7 pb-32 bg-hero-pattern bg-cover">

      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">
          IP Address Tracker
        </h1>
        <div class="flex">
          <input 
            v-model="queryIp"
            class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
            type="text"
            placeholder="Search for any IP address or leave empty to get your ip info"
          >
          <div class="flex cursor-pointer bg-black text-white rounded-tr-md rounded-br-md px-4 items-center">
            <ChevronRightIcon
              @click="getIpInfo"
              size="40" 
              class="" 
            />
          </div>
        </div>
      </div>

      <IPInfo 
        v-if="ipInfo"
        :ipInfo="ipInfo"        
      />
    </div>
    <div 
      id="map" 
      class="h-full z-10" 
    />
  </div>
</template>

<script setup>
import {  ref, onMounted } from "vue"

import "leaflet/dist/leaflet.css"
import * as L from 'leaflet'
import axios from 'axios'

import IPInfo from '@/components/IPInfo.vue';
import ChevronRightIcon from 'vue-material-design-icons/ChevronRight.vue'

const queryIp = ref("")
const ipInfo = ref(null)
let map

onMounted(async () => {
  map = L
    .map('map', {
      zoomControl: false,
      preferCanvas: true,
      attributionControl: false,
      bounceAtZoomLimits: false
    })
    .setView([36.287938, 59.6131317], 12)

  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 18,
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map)

})

const getIpInfo = async () => {
  try {
    const data = await axios.get(`https://geo.ipify.org/api/v1?apiKey=at_OOV8MuA6k1oMoTUgOyZjPJpp3lmAY&ipAddress=${ queryIp.value }`, {
    })
    const result = data.data
    console.log('result', result);
    ipInfo.value = result

    L.marker([ipInfo.value.location.lat, ipInfo.value.location.lng]).addTo(map);
    map.flyTo([ipInfo.value.location.lat, ipInfo.value.location.lng], 14);
  } catch (error) {
    console.log('error', error);
  }
}
</script>

<style lang="sass">
 
</style>