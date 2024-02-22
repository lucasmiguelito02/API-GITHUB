<script setup>
import { ref } from 'vue';
import CompositionApi from './components/CompositionApi.vue'

const isOpen = ref(true)
</script>

<template>
  <input type="checkbox" v-model="isOpen"> {{ isOpen }}
  <CompositionApi v-if="isOpen" />
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