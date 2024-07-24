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

    <div v-for="day in props.place.forecast.forecastday" :key="day">
      <WeatherForceCastDay :forcast="day" />
    </div>

    <div v-show="showDetails">
      <WeatherInfo
        :info="props.place.current"
        @close-info="showDetails = !showDetails"
        @removePlace="removePlace"
      />
    </div>

    <div class="flex justify-end items-center gap-1 mt-10">
      <button @click="showDetails = !showDetails">
        More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import BorderLine from './BorderLine.vue'
import WeatherForceCastDay from './WeatherForceCastDay.vue'
import WeatherInfo from './WeatherInfo.vue'

const props = defineProps({
  place: Object
})

const showDetails = ref(false)
</script>

<style scoped></style>
