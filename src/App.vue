<script setup>
import Profile from './components/Profile.vue';
import { ref } from 'vue';
const isOpen = ref(true)
</script>

<template>
  <Profile />
</template>

<style>
#app {
  font-family: 'Ubuntu', sans-serif;
  min-height: 100vh;
  max-width: 40rem;
  margin: 0 auto;
  text-align: center;
}
</style>