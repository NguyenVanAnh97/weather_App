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
      <WeatherCar :place="place" @delete-place="deletePlace" />
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

const deletePlace = (name) => {
  places.value = places.value.filter((place) => place.location.name !== name) //  tạo ra một mảng mới với tất cả các phần tử của mảng hiện tại thỏa mãn điều kiện được chỉ định.
} // truyền emit từ component weatherInfo => weatherCar => App (App render weatherCar dựa vào data places mà SearchInput emit lên)

/* 1. Hàm filter duyệt qua từng đối tượng place trong mảng places.value.
   2. Nó kiểm tra xem place.location.name có khác với name hay không.
   3. Nếu place.location.name khác với name, đối tượng đó sẽ được giữ lại trong mảng mới.
   4. Nếu place.location.name trùng với name, đối tượng đó sẽ bị loại bỏ khỏi mảng mới. */
</script>

<style scoped></style>
