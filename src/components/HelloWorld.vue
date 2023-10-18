// File: ./src/components/HelloWorld.vue

<script setup>
  import { onMounted, ref } from 'vue'
  import axios from 'axios'
  const server = import.meta.env.VITE_SERVER
  const port = import.meta.env.VITE_API_PORT ? ':' + import.meta.env.VITE_API_PORT : ''

  const helloString = ref('...')
  // File: ./src/components/HelloWorld.vue

onMounted(async () => {
  const {data} = await axios.get(`${server}${port}/api/hello`)
  helloString.value = data.helloString
})
</script>

<template>
    <h1>{{ helloString }}</h1>
</template>

