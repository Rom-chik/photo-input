<script setup lang="ts">
import {reactive, ref} from "vue";


const userData = reactive({
  username: '',
  password: ''
});

const onButtonClick = (async() => {
  console.log('data submitted', userData)
});

</script>

<template>

  <!-- username input -->
  <div class="relative">
      <input id="username" type="text" v-model="userData.username" class="w-[250px] h-[35px] peer focus:outline-none border-2 border-black focus:border-sky-500 " placeholder=" "/>
      <label for="username" class="absolute left-1 -top-6 peer-placeholder-shown:top-1 peer-focus:-top-6 transition-all duration-75" >Username</label>
  </div>
  <!-- password input -->
  <div class="relative">
      <input id="password" type="password" v-model="userData.password" class="w-[250px] h-[35px] peer focus:outline-none border-2 border-black focus:border-sky-500 " placeholder=" "/>
      <label for="password" class="absolute left-1 -top-6 peer-placeholder-shown:top-1 peer-focus:-top-6 transition-all duration-75" >Password</label>
  </div>
  <!-- submit button -->
  <div>
      <button @click="onButtonClick()" type="submit" class="border border-black hover:bg-[#F0F0F0] w-[75px] h-[35px]">Submit</button>
  </div>

</template>

<style scoped>

</style>