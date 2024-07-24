<script setup lang="ts">
import {reactive, ref} from "vue";


const userData = reactive({
  username: '',
  password: '',
  icon: null
});

const onButtonClick = (async() => {
    console.log('data submitted', userData)
});

const fileInput = ref<HTMLInputElement | null>(null);
const imagePreviewUrl = ref<string | ArrayBuffer | null>(null);
const fullScaleImage = ref<string | ArrayBuffer | null>(null);

const readFileIfPresent = (input, files) => {
  if (files && files[0]) {
    const reader = new FileReader();
    reader.onload = (e) => {
      userData.icon = files;
      imagePreviewUrl.value = e.target?.result;
    };
    reader.readAsDataURL(files[0]);
  }
};
const pickFile = (event: Event) => {
  const input = event.target as HTMLInputElement;
  const files = input.files;
  readFileIfPresent(input, files);
};

const toggleFullScaleImage = () => {
  if(fullScaleImage.value) {
    fullScaleImage.value = null
  } else {
    fullScaleImage.value = imagePreviewUrl.value;
  }
};


</script>

<template>
  <div class="flex justify-center items-center w-1/4 min-w-72 h-2/3 bg-[white]">
    <div class="flex flex-col gap-6 justify-center items-center">

        <h3 class="text-2xl">Fill out the information</h3>

        <div></div>

        <!-- input profile photo by clicking -->
        <label for="fileInput" class="relative cursor-pointer">
            <!-- insert profile photo over of svg -->
            <div v-if="imagePreviewUrl" class="preview">
                <img :src="imagePreviewUrl" alt="Image Preview" class="absolute rounded-full object-cover w-[100px] h-[100px]" />
            </div>
            <!-- default svg icon TODO v-else instead of overlaying with absolut-->
            <svg viewBox="-3.6 -3.6 31.20 31.20" fill="none" class="w-[100px] h-[100px]">
                <rect x="-3.6" y="-3.6" width="31.20" height="31.20" rx="15.6" fill="#d1d5db" ></rect>
                <path d="M12.1992 12C14.9606 12 17.1992 9.76142 17.1992 7C17.1992 4.23858 14.9606 2 12.1992 2C9.43779 2 7.19922 4.23858 7.19922 7C7.19922 9.76142 9.43779 12 12.1992 12Z" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
                <path d="M3 22C3.57038 20.0332 4.74796 18.2971 6.3644 17.0399C7.98083 15.7827 9.95335 15.0687 12 15C16.12 15 19.63 17.91 21 22" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
            </svg>
            <!-- small clickable svg icon below TODO remake with peer instead of usual hover: -->
            <svg fill="#000000" viewBox="-4.8 -4.8 41.60 41.60" preserveAspectRatio="xMidYMid" class="w-[32px] h-[32px] absolute left-8 top-20 ">
                <rect x="-4.8" y="-4.8" width="41.60" height="41.60" rx="20.8" fill="#d1d5db" class="hover:fill-gray-400 transition duration-75"></rect>
                <path d="M29.000,26.000 L3.000,26.000 C1.346,26.000 -0.000,24.654 -0.000,23.000 L-0.000,7.000 C-0.000,5.346 1.346,4.000 3.000,4.000 L7.381,4.000 L9.102,0.554 C9.270,0.214 9.617,0.000 9.996,0.000 L22.006,0.000 C22.385,0.000 22.731,0.214 22.901,0.554 L24.619,4.000 L29.000,4.000 C30.654,4.000 32.000,5.346 32.000,7.000 L32.000,23.000 C32.000,24.654 30.654,26.000 29.000,26.000 ZM30.000,7.000 C30.000,6.449 29.551,6.000 29.000,6.000 L24.000,6.000 C23.950,6.000 23.907,5.979 23.859,5.972 C23.788,5.961 23.717,5.955 23.649,5.929 C23.588,5.906 23.537,5.869 23.482,5.834 C23.428,5.801 23.373,5.773 23.326,5.729 C23.273,5.680 23.235,5.620 23.194,5.560 C23.166,5.520 23.127,5.491 23.105,5.446 L21.387,2.000 L10.615,2.000 L8.895,5.446 C8.848,5.541 8.785,5.623 8.715,5.695 C8.701,5.710 8.684,5.719 8.669,5.733 C8.597,5.798 8.518,5.851 8.432,5.892 C8.403,5.907 8.375,5.919 8.344,5.931 C8.234,5.971 8.120,5.999 8.002,6.000 C8.001,6.000 8.001,6.000 8.000,6.000 L3.000,6.000 C2.449,6.000 2.000,6.449 2.000,7.000 L2.000,23.000 C2.000,23.551 2.449,24.000 3.000,24.000 L29.000,24.000 C29.551,24.000 30.000,23.551 30.000,23.000 L30.000,7.000 ZM16.000,21.000 C12.140,21.000 9.000,17.860 9.000,14.000 C9.000,10.140 12.140,7.000 16.000,7.000 C19.860,7.000 23.000,10.140 23.000,14.000 C23.000,17.860 19.860,21.000 16.000,21.000 ZM16.000,9.000 C13.243,9.000 11.000,11.243 11.000,14.000 C11.000,16.757 13.243,19.000 16.000,19.000 C18.757,19.000 21.000,16.757 21.000,14.000 C21.000,11.243 18.757,9.000 16.000,9.000 Z"></path>
            </svg>
            <!-- input over big and small icon -->
            <input ref="fileInput" id="fileInput" type="file" @input="pickFile" class="absolute inset-0 w-full h-full opacity-0 pointer-events-none">

            <!-- open button -->
            <button @click="toggleFullScaleImage()" class="absolute left-24 top-9 w-[32px] h-[32px]">
                <svg viewBox="-4.2 -4.2 29.40 29.40" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0">
                    <rect class="hover:fill-gray-400 transition duration-75" x="-4.2" y="-4.2" width="29.40" height="29.40" rx="14.7" fill="#d1d5db" strokewidth="0"></rect></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"><g fill="none" fill-rule="evenodd" stroke="#000000" stroke-linecap="round" stroke-linejoin="round" transform="translate(1 2)">
                    <path d="m.5.5v16.021"></path> <path d="m18.5.5v16.021"></path> <path d="m12.507 12.515 4-4-4-4.015"></path> <path d="m6.507 12.515-4-4 4-4.015"></path> <path d="m16.5 8.5h-14"></path> </g> </g>
                </svg>
            </button>
        </label>

        <!-- open or close image in full scale -->
        <div v-if="fullScaleImage" class="preview absolute inset-0 flex justify-center items-center bg-black bg-opacity-50 z-50">
            <img :src="fullScaleImage" alt="Full scale image" class="max-w-full max-h-full" />
        <!-- close button -->
            <button @click="toggleFullScaleImage" class="absolute top-4 w-[64px] h-[64px]">
                <svg viewBox="-3.6 -3.6 31.20 31.20" fill="none"><g id="SVGRepo_bgCarrier" stroke-width="0">
                    <rect x="-3.6" y="-3.6" width="31.20" height="31.20" rx="15.6" fill="#d1d5db" strokewidth="0"></rect></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier">
                    <path d="M20.7457 3.32851C20.3552 2.93798 19.722 2.93798 19.3315 3.32851L12.0371 10.6229L4.74275 3.32851C4.35223 2.93798 3.71906 2.93798 3.32854 3.32851C2.93801 3.71903 2.93801 4.3522 3.32854 4.74272L10.6229 12.0371L3.32856 19.3314C2.93803 19.722 2.93803 20.3551 3.32856 20.7457C3.71908 21.1362 4.35225 21.1362 4.74277 20.7457L12.0371 13.4513L19.3315 20.7457C19.722 21.1362 20.3552 21.1362 20.7457 20.7457C21.1362 20.3551 21.1362 19.722 20.7457 19.3315L13.4513 12.0371L20.7457 4.74272C21.1362 4.3522 21.1362 3.71903 20.7457 3.32851Z" fill="#0F0F0F"></path> </g>
                </svg>
            </button>
        </div>


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

    </div>
  </div>
</template>

<style scoped>

</style>