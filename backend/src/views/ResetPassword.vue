<template>
  <div class="flex min-h-full flex-1 flex-col justify-center px-6 py-12 lg:px-8">
 <guest-layout title="Set new Password">
    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form class="space-y-6" action="#" method="POST">
        <input type="hidden" name="remember" value="true">
        <div>
          <div class="flex items-center justify-between">
            <label for="newPassword" class="sr-only">New Password</label>
          </div>
          <div class="mt-2">
            <input
            id="newPassword"
            placeholder="New Password"
            name="newPassword"
            type="password"
            autocomplete="current-password" required=""
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>
        <div>
          <div class="flex items-center justify-between">
            <label for="passwordRepeat" class="sr-only">Repeat Password</label>
          </div>
          <div class="mt-2">
            <input
             id="passwordRepeat"
             placeholder="Repeat Password"
             name="passwordRepeat"
             type="password"
             autocomplete="current-password" required=""
             class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div>
          <button type="submit" class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Submit</button>
        </div>
      </form>

      <p class="mt-10 text-center text-sm">
        <!-- <a href="/login" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500"> </a> -->
        <router-link :to = "{name: 'login'}" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">Go Back to Login</router-link>
      </p>
    </div>
</guest-layout>
  </div>
</template>

<script setup>
import GuestLayout from '../components/GuestLayout.vue';
</script>

<style lang="scss" scoped></style>
