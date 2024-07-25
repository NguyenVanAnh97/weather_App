<template>
  <div class="mb-2 flex items-center justify-center">
    <table class="w-full">
      <tr>
        <td class="w-1/3">
          {{ new Date(forcast.date).toLocaleDateString('en-us', { weekday: 'long' }) }}
        </td>

        <td class="w-1/3">
          <img :src="props.forcast.day.condition.icon" alt="icon" width="30" class="mx-auto" />
        </td>

        <td class="w-1/3 text-right">
          {{ Math.round(props.forcast.day.maxtemp_c) }} /
          {{ Math.round(props.forcast.day.mintemp_c) }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script setup>
const props = defineProps({
  forcast: Object
})
</script>

<style scoped></style>
