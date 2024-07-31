<script setup lang="ts">
import PhotoInput from './components/PhotoInput.vue'
import UserDataInput from './components/UserDataInput.vue'


</script>

<template>
  <div class="flex flex-col justify-center items-center w-full h-[100vh] bg-[#F0F0F0]">
    <div id="card-1" class="flex justify-center items-center w-1/4 min-w-72 h-2/3 bg-[white]">
        <div class="flex flex-col gap-6 justify-center items-center">

            <h3 class="text-2xl">Fill out the information</h3>

            <div></div>

            <PhotoInput />

            <div></div>

            <UserDataInput />

        </div>
    </div>

  </div>
</template>

<style scoped>

</style>