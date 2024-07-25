<template>
  <div
    class="absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8"
  >
    <div class="flex justify-end mb-10">
      <button @click="emitEven" class="p-1">
        <i class="fa-solid fa-xmark text-xl"></i>
      </button>
    </div>

    <div class="flex items-start justify-between gap-6 mb-20">
      <div class="text-center flex-1">
        <i class="fa-solid fa-wind text-2xl"></i>
        <p class="text-xl font-bold">{{ props.info.current.wind_kph }}</p>
        <p>Gió</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-droplet mb text-2xl"></i>
        <p class="text-xl font-bold">{{ props.info.current.humidity }}%</p>
        <p>Độ ẩm</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-umbrella mb text-2xl"></i>
        <p class="text-xl font-bold">{{ props.info.current.precip_in }} mm</p>
        <p>Lượng mưa</p>
      </div>
    </div>

    <div class="flex justify-between items-start gap-6 mb-10">
      <div class="text-center flex-1">
        <i class="fa-solid fa-fan mb text-2xl"></i>
        <div class="text-xl font-bold">{{ props.info.current.wind_degree }}</div>
        <p>Hướng gió</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-temperature-half mb text-2xl"></i>
        <div class="text-xl font-bold">{{ props.info.current.feelslike_c }}</div>
        <p>Cảm nhận thực tế</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-sun mb text-2xl"></i>
        <div class="text-xl font-bold">{{ props.info.current.uv }}</div>
        <p>Chỉ số tia UV</p>
      </div>
    </div>

    <div class="flex justify-between items-center">
      <h3 class="text-slate-900/50">Cập nhật lần cuối : {{ props.info.current.last_updated }}</h3>

      <button @click="$emit('remove-place')">
        <i class="fa-solid fa-trash"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  info: Object
})

const emit = defineEmits(['close-info', 'remove-place']) // truyền emit ra component cha

const emitEven = () => {
  emit('close-info', true)
}
</script>
