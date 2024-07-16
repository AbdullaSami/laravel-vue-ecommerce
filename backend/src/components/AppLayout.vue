<template>
  <div class="w-screen h-screen flex">
    <!-- Side Bar -->

    <Sidebar :class="{'-ml-[160px]': !sidebarOpened}" />

    <!-- NavBar -->
    <div class="flex-1">
      <NavBar @toggle-sidebar="toggleSidebar"></NavBar>
      <!--      Content-->
      <main class="p-6">
        <router-view></router-view>
      </main>
      <!--      Content-->
    </div>

  </div>

</template>

<script setup>
import {ref, computed, onMounted, onUnmounted} from 'vue'
import Sidebar from "./Sidebar.vue";
import NavBar from "./NavBar.vue";
import store from "../store";

// Sidebar toggler function
const sidebarOpened = ref(true)
function toggleSidebar(){
    console.log('sidebarOpened');
    sidebarOpened.value = !sidebarOpened.value;
}
function updateSidebarState(){
    sidebarOpened.value = window.outerWidth>768 ;
}

onMounted(()=>{
    updateSidebarState();
    window.addEventListener('resize',updateSidebarState);
})

onUnmounted(() => {
  window.removeEventListener('resize', updateSidebarState)
})
</script>

<style lang="scss" scoped></style>
