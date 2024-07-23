<template>
  <div class="text-center mb-6">
    <h1>{{  new Date().toLocaleDateString('en-us', {
      weekday: 'long',
      year: 'numeric',
      month: 'short',
      day: 'numeric'
    }) }}</h1>
  </div>

  <div>
    <SeachInput />
  </div>
</template>

<script setup>
  import SeachInput from './components/SeachInput.vue';
</script>

<style scoped>

</style>