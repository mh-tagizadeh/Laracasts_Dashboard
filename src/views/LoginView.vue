<template>
   <div class="h-screen w-screen flex items-center justify-center">
      <div class="w-full max-w-sm mx-auto overflow-hidden bg-white rounded-lg shadow-md dark:bg-gray-800">
         <div class="px-6 py-4">
            <h2 class="text-3xl font-bold text-center text-gray-700 dark:text-white">Brand</h2>

            <h3 class="mt-1 text-xl font-medium text-center text-gray-600 dark:text-gray-200">Welcome Back</h3>

            <p class="mt-1 text-center text-gray-500 dark:text-gray-400">Login or create account</p>

            <form @submit.prevent="submit">
               <div class="w-full mt-4">
                  <input
                     class="block w-full px-4 py-2 mt-2 text-gray-700 placeholder-gray-500 bg-white border rounded-md dark:bg-gray-800 dark:border-gray-600 dark:placeholder-gray-400 focus:border-blue-400 dark:focus:border-blue-300 focus:ring-opacity-40 focus:outline-none focus:ring focus:ring-blue-300"
                     type="text" placeholder="Username" aria-label="Username" v-model="user.username" />
               </div>

               <div class="w-full mt-4">
                  <input
                     class="block w-full px-4 py-2 mt-2 text-gray-700 placeholder-gray-500 bg-white border rounded-md dark:bg-gray-800 dark:border-gray-600 dark:placeholder-gray-400 focus:border-blue-400 dark:focus:border-blue-300 focus:ring-opacity-40 focus:outline-none focus:ring focus:ring-blue-300"
                     type="password" placeholder="Password" aria-label="Password" v-model="user.password" />
               </div>

               <div class="flex items-center justify-between mt-4">
                  <a href="#" class="text-sm text-gray-600 dark:text-gray-200 hover:text-gray-500">Forget Password?</a>

                  <button
                     class="px-4 py-2 leading-5 text-white transition-colors duration-300 transform bg-gray-700 rounded hover:bg-gray-600 focus:outline-none"
                     type="submit">Login</button>
               </div>
            </form>
         </div>

         <div class="flex items-center justify-center py-4 text-center bg-gray-50 dark:bg-gray-700">
            <span class="text-sm text-gray-600 dark:text-gray-200">Don't have an account? </span>

            <a href="#" class="mx-2 text-sm font-bold text-blue-500 dark:text-blue-400 hover:underline">Register</a>
         </div>
      </div>
   </div>
</template>

<script setup>
import { useUserStore } from '../stores/user';
import { ref } from 'vue';

const store = useUserStore()

const user = {
   username: '',
   password: '',
};
const errorMsg = ref('');

const submit = async () => {
   store.login(user)
      .then(() => console.log('Success!'))
      .catch(err => {
         errorMsg.value = err.response.data.error
         console.log(err)
      })
}
</script>
