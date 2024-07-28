<template>
  <div>
    <form>
      <div class="bg-white border border-indigo-600/30 rounded-lg drop-shadow-lg flex items-center">
        <i class="fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
        <input
          type="text"
          placeholder="Search for a place"
          class="rounded-r-lg border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset p-2 w-full"
          v-model="searchTerm.query"
          @input="handleSearch"
        />
      </div>
    </form>

    <div class="bg-white my-2 rounded-lg shadow-lg">
      <div v-if="searchTerm.results !== null">
        <div v-for="place in searchTerm.results" :key="place.name">
          <button
            class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left"
            @click="getWeather(place.id)"
          >
            {{ place.name }} , {{ place.region }} , {{ place.country }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const searchTerm = reactive({
  query: '',
  timeout: null,
  results: null
})

const handleSearch = () => {
  clearTimeout(searchTerm.timeout) // Giảm Số Lần Gọi API Không Cần Thiết, giảm áp lực lên hệ thống backend
  searchTerm.timeout = setTimeout(async () => {
    if (searchTerm.query !== '') {
      const response = await fetch(
        `http://api.weatherapi.com/v1/search.json?key=834afe3d28d04f2d9ea165725242207&q=${searchTerm.query}`
      )

      const data = await response.json()
      searchTerm.results = data
    } else {
      searchTerm.results = null
    }
  }, 500)
}

const emit = defineEmits(['place-data']) //phải emit data lên component cha để hiển thị data trên đó
// component con này đơn giản chỉ để lấy dữ liệu

const getWeather = async (id) => {
  const response = await fetch(
    `http://api.weatherapi.com/v1/forecast.json?key=834afe3d28d04f2d9ea165725242207&q=id:${id}&days=3&aqi=no&alerts=no`
  )

  const data = await response.json()
  emit('place-data', data) // emit data lên component cha

  searchTerm.query = ''
  searchTerm.results = null
}
</script>

<style scoped></style>
