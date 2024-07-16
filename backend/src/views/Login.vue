<template>
  <guest-layout title="Sign in to your account">
    <form class="space-y-6" method="POST" @submit.prevent="login">
        <!-- Error message -->
        <div v-if="errorMsg" class="flex items-center justify-between py-3 px-5 bg-red-500 text-white rounded">
            {{ errorMsg }}
            <span
            @click="errorMsg=''"
            class="w-8 h-8 flex items-center justify-center  rounded-full transition-colors cursor-pointer hover:bg-[rgba(0,0,0,0.2)]"
            >

            <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>

            </span>
        </div>
    <div class="mt-4 sm:mx-auto sm:w-full sm:max-w-sm">
        <div>
          <label for="email-address" class="sr-only">Email address</label>
          <div class="mt-2">
            <input id="email-address" placeholder="Email address" name="email" type="email" autocomplete="email" required="" v-model="user.email" class="block w-full rounded-t-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div class="w-full">
          <div class="flex items-center justify-between">
            <label for="password" class="sr-only">Password</label>
          </div>
          <div>
            <input id="password" placeholder="Password" name="password" type="password" autocomplete="current-password" required=""
            v-model="user.password"
            class="block w-full rounded-b-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>

          <div class="mt-5 flex items-center justify-between mt-2">
            <div class="flex items-center">
                <input id="remember-me" name="remember-me" type="checkbox"
                class="h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded"
                value="false"
                v-model="user.remember"
                />
                <label for="remember-me" class="ml-2 block text-sm text-gray-900">Remember me</label>
                <div class="text-sm">
              <router-link :to="{name: 'request-password'}" class="ml-4 font-semibold text-indigo-600 hover:text-indigo-500">Forgot password?</router-link>
            </div>
            </div>
          </div>
        </div>

        <div>
          <button type="submit"
          :disabled="loading"
          class="group relative mt-5 flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          :class="{
            'cursor-not-allowed opacity-50': loading,
            'hover:bg-indigo-500': loading,
          }">
          <svg
            v-if="loading"
            class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
          >
            <circle
              class="opacity-25"
              cx="12"
              cy="12"
              r="10"
              stroke="currentColor"
              stroke-width="4"
            ></circle>
            <path
              class="opacity-75"
              fill="currentColor"
              d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
            ></path>
          </svg>
          <span class="absolute left-0 inset-y-0 flex items-center pl-3">
              <LockClosedIcon class="h-5 w-5 text-indigo-500 group-hover:text-indigo-400" aria-hidden="true"/>
            </span>
          Sign in
          </button>
        </div>

      <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        {{ ' ' }}
        <a href="#" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">Start a 14 day free trial</a>
      </p>
    </div>
    </form>
    </guest-layout>
</template>

<script setup>
import {ref} from "vue";
import { LockClosedIcon } from "@heroicons/vue/24/outline";
import GuestLayout from "../components/GuestLayout.vue";
import store from "../store";
import router from "../router";

let loading = ref(false);
let errorMsg = ref("");

const user = {
    email: "",
    password: "",
    remember: "",
};

function login(){
    loading.value = true;
    store.dispatch('login', user)
    .then(()=>{
        loading.value = false;
        router.push({name: 'app.dashboard'})
    })
    .catch(({response})=>{
        loading.value = false;
        errorMsg.value = response.data.message;
    })
}
</script>

<style lang="scss" scoped></style>
