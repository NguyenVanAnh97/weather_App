<template>
  <div class="text-white p-10 rounded-lg shadow-lg gap-6 relative overflow-hidden bg-blue-400">
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot"></i>
        <h1 class="text-3xl">{{ props.place.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-clock"></i>
        <h1 class="text-3xl">
          {{ new Date(props.place.location.localtime).getHours() }}:{{
            new Date(props.place.location.localtime).getMinutes()
          }}
        </h1>
      </div>
    </div>

    <div class="text-center flex-1">
      <img :src="props.place.current.condition.icon" alt="icon" width="100" class="mx-auto" />
      <h1 class="text-9xl mb-2 -mr-2">{{ Math.round(props.place.current.temp_c) }}&deg;</h1>
      <p class="text-2xl">{{ props.place.current.condition.text }}</p>
    </div>

    <BorderLine />
  </div>
</template>

<script setup>
import BorderLine from './BorderLine.vue'

const props = defineProps({
  place: Object
})

console.log(props.place)
</script>

<style scoped></style>
