<template>
    <div class="pt-16">
        <h1 class="text-3xl font-semibold mb-4">Enter your phone number</h1>
        <form action="#" @submit.prevent="handleLogin">
            <div class="overflow-hidden shadow sm:rounded-md max-w-sm mx-auto text-left">
                <div class="bg-white px-4 py-5 sm:p-6">
                    <div>
                        <input type="text" v-maska data-maska="## ### ######" v-model="credentials.phone" name="phone" id="phone" placeholder=" 07 123 456789"
                        class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:border-black focus:outline-none">
                    </div>
                </div>
                <div class="bg-gray-50 px-4 py-3 text-right sm:px-6">
                    <button type="submit" @submit.prevent="handleLogin"
                        class="inline-flex justify-center rounded-md border border-transparent bg-black py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-gray-600 focus:outline-none">Continue</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script setup>
    import {vMaska} from 'maska'
    import {reactive} from 'vue'
    import axios from 'axios'

    const credentials = reactive({
        phone: null
    })

    const api = axios.create({
  baseURL: 'https://swiftride.000webhostapp.com'
});

const handleLogin = () => {
  if (credentials && credentials.phone) {
    const formattedPhone = credentials.phone.replace(/\s/g, '').replace(/\(/g, '').replace(/\)/g, '').replace(/-/g, '');
    api.post('/login', {
      phone: formattedPhone
    })
    .then((response) => {
      console.log(response.data);
    })
    .catch((error) => {
      console.log(error);
      alert(error.response.data.message);
    });
  } else {
    console.error('Invalid phone number provided.');
  }
};
</script>

<style>

</style>