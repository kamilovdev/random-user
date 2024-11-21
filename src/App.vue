<script setup>
import { ref, computed } from 'vue';

const firstname = ref("Diana");
const lastname =  ref("Richards");
const email = ref("diana.richards@example.com");
const gender = ref("female");
const phoneNumber = ref("(350) 931-3451");
const img = ref("https://randomuser.me/api/portraits/women/66.jpg")

const fullname = computed(() => `${firstname.value} ${lastname.value}`)

const rendomUser = async () => {
 try {
   const res = await fetch('https://randomuser.me/api/');
    if (!res.ok){
      throw new Error(`Server error: ${res.status}`);
    }

    const { results } = await res.json();
    const user = results[0];
 

    firstname.value = user.name.first;
    lastname.value = user.name.last;
    email.value = user.email;
    gender.value = user.gender;
    phoneNumber.value = user.phone;
    img.value = user.picture.large;

  } catch (error) {
       console.log("error", error);
  }
}
</script>

<template>
  <div class="flex justify-center items-center min-h-screen">
     <div class="flex flex-col justify-center items-center">
             <div class="relative mb-8">
                  <div
                  class=" absolute left-1/2 -top-2 bg-white rounded-full px-4 text-lg transform -translate-x-1/2"
                  >
                     {{gender}}
                  </div>
                  <img 
                  class="w-64 h-64 rounded-full border-8"
                  :class= "gender === 'male' ? 'border-blue-500' : 'border-pink-500'"
                  :src="img"
                  :alt="img">
             </div>

             <div class="flex flex-col text-center space-y-1 gap-3">
              <h1 class="text-4xl font-bold">{{ fullname }}</h1>
              <p class="text-lg text-gray-500">{{email}}</p>
              <p class="text-lg text-gray-500">{{phoneNumber}}</p>
 
            <div>
              <button
               @click="rendomUser"
               class="bg-black text-white px-6 py-2 rounded font-bold mt-6">
                Random user
              </button>
            </div>
             </div>
     </div>
  </div>
</template>

<style scoped>
</style>