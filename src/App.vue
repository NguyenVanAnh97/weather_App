<template>
  <div class="text-center mb-6">
    <h1>
      {{
        new Date().toLocaleDateString('en-us', {
          weekday: 'long',
          year: 'numeric',
          month: 'short',
          day: 'numeric'
        })
      }}
    </h1>
  </div>

  <div>
    <SeachInput @place-data="addPlace" class="mb-3" />
  </div>

  <div class="grid grid-cols-2 gap-4">
    <div v-for="place in places" :key="place.name">
      <WeatherCar :place="place" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import SeachInput from './components/SeachInput.vue'
import WeatherCar from './components/WeatherCar.vue'

const places = ref([])

const addPlace = (data) => {
  places.value.push(data) // push data lên component cha
}

console.log(places)
</script>

<style scoped></style>
