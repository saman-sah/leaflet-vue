<template>
  <div class="absolute -bottom-64 z-50 lg:-bottom-20 flex flex-col lg:flex-row bg-white gap-y-4 gap-x-12 px-8 pt-8 pb-12 rounded-md">
    
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">IP Address</h3>
      <span class="text-2xl">
        {{ ipInfo.ip }}
      </span>
    </div>
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Location</h3>
      <span class="text-2xl">
        {{   ipInfo.location.region }} 
      </span>
    </div>
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Timezone</h3>
      <span class="text-2xl">UTC {{ ipInfo.location.timezone }}</span>
    </div>
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">ISP</h3>
      <span class="text-2xl">{{ ipInfo.isp }}</span>
    </div>

  </div>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps({
  ipInfo: {
    type: Object,
    default: () => {}
  }
})
</script>