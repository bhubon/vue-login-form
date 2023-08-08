<script setup>

// import { WelcomeComponent } from './components/WelcomeComponent.vue';

import { ref, reactive } from 'vue'
const userList = reactive({
  name: '',
  password: '',
  confirmPassword: ''
})
const registerMode = ref(false);
const isLogin = ref(false);
const message = ref('');

const userInputs = reactive({
  name: '',
  password: '',
  confirmPassword: ''
})
const loggedInUserName = ref('');

function processData() {
  message.value = ''
  let getUser = JSON.parse(localStorage.getItem('user'))
  if (registerMode.value) {
    //register user
    if (userList.password != userList.confirmPassword) {
      message.value = "Password does not match"
    } else {
      if (getUser && userInputs.name == getUser.name) {
        message.value = "Username already exists!"
        return;
      }
      localStorage.setItem('user', JSON.stringify(userInputs));
      userInputs.name = ''
      userInputs.password = ''
      userInputs.confirmPassword = ''
      registerMode.value = false;
      message.value = "Successfully Registered! Please login!"
    }
  } else {
    // login user
    if (getUser.name == userInputs.name && getUser.password == userInputs.password) {
      isLogin.value = true;
      message.value = "Successfully login!";
      loggedInUserName.value = getUser.name
      userInputs.name = ''
      userInputs.password = ''
      userInputs.confirmPassword = ''
    } else {
      message.value = "Invalid login credential!"
    }
  }
}

function logOut() {
  isLogin.value = false;
  loggedInUserName.value = '';
}

</script>

<template>
  <section class="flex h-screen w-full">
    <div class="w-1/2"
      style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
      <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">Kosmos!</h1>
    </div>
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200" v-show="!isLogin">
      <h2 class="mb-5 text-xl">Login or register</h2>
      <div class="w-full max-w-xs">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Username
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username" type="text" placeholder="Username" v-model="userInputs.name">
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
              Password
            </label>
            <input
              class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="password" type="password" placeholder="******************" v-model="userInputs.password">
            <!-- <p class="text-red-500 text-xs italic">Please choose a password.</p> -->
          </div>
          <div class="mb-6" v-show="registerMode">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="confirm_password">
              Confirm Password
            </label>
            <input
              class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="confirm_password" type="password" placeholder="******************" v-model="userInputs.confirmPassword">
            <!-- <p class="text-red-500 text-xs italic">Please choose a password.</p> -->
          </div>
          <div class="flex items-center justify-between">
            <button
              class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="button" v-show="!registerMode" @click.prevent="processData()">
              Sign In
            </button>
            <button
              class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="button" v-show="registerMode" @click="processData()">
              Sign Up
            </button>
            <a class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800" href="#"
              @click.prevent="registerMode = !registerMode" v-show="!registerMode">
              Or Register
            </a>
            <a class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800" href="#"
              @click.prevent="registerMode = !registerMode" v-show="registerMode">
              Or Login
            </a>
          </div>
          <div class="flex items-center justify-center">
            <p class="mt-5 text-gray-600 text-sm" v-show="message">{{ message }}</p>
          </div>
        </form>
        <p class="text-center text-gray-500 text-xs">
          &copy;2023 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200" v-show="isLogin">
      <h2 class="mb-5 text-xl">You have logged in successfully!</h2>
      <div class="w-full max-w-xs text-center ">
        <h3 class="font-bold mb-7 text-green-700">Welcome, {{ loggedInUserName }}</h3>
        <button
          class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline text-center mb-5"
          type="button" @click.prevent="logOut()">
          Logout
        </button>
        <p class="text-center text-gray-500 text-xs">
          &copy;2023 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
  </section>
</template>
<style scoped></style>