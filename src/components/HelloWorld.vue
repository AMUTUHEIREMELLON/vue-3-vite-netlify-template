// File: ./src/components/HelloWorld.vue

<script setup>
  import { onMounted, ref } from 'vue'
  import axios from 'axios'
  const server = import.meta.env.VITE_SERVER
  const port = import.meta.env.VITE_API_PORT ? ':' + import.meta.env.VITE_API_PORT : ''

  const helloString = ref('...');
  const newHelloString = ref('');

onMounted(async () => {
  const {data} = await axios.get(`${server}${port}/api/hello`)
  helloString.value = data.helloString
})
async function submitForm (){
  try{
    const response = await axios.post(`${server}${port}/api/hello`, { newHelloString: newHelloString.value });
    console.log('POST request successful:', response.data);
    newHelloString.value = '';
  } catch (error){
    console.error('Error sending POST request:', error);
  }
};
</script>


<template>
  <div>
    <h1>{{ helloString }}</h1>
    <input
      type="text"
      id="helloinput"
      v-model="newHelloString"
    />
    <button @click="submitForm">Submit</button>
  </div>
</template>
