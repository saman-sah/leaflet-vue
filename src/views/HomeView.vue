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
            class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
            type="text"
            placeholder="Search for any IP address or leave empty to get your ip info"
          >
          <div class="flex cursor-pointer bg-black text-white rounded-tr-md rounded-br-md px-4 items-center">
            <ChevronRightIcon 
              size="40" 
              class="" 
            />
          </div>
        </div>
      </div>

      <IPInfo />
    </div>
    <div id="map" class="h-full z-10"></div>
  </div>
</template>

<script setup>
import {  onMounted } from "vue"

import "leaflet/dist/leaflet.css"
import * as L from 'leaflet'

import ChevronRightIcon from 'vue-material-design-icons/ChevronRight.vue'

import IPInfo from '@/components/IPInfo.vue';

onMounted(async () => {
  const map = L
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
</script>

<style lang="sass">
 
</style>