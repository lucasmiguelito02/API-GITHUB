<script setup>
import { ref } from 'vue';
import Profile from './components/Profile.vue'

const isOpen = ref(true)
</script>

<template>
  <input type="checkbox" v-model="isOpen"> {{ isOpen }}
  <Profile v-if="isOpen">
    <h1>GitHub User Data</h1>
    <template v-slot:footer>
      <footer>
        Desenvolvido por <a href="https://github.com/isaacpontes" target="_blank">Isaac Pontes</a>
      </footer>
    </template>
  </Profile>
</template>

<style>
#app {
  font-family: 'Ubuntu', sans-serif;
  min-height: 100vh;
  max-width: 40rem;
  margin: 0 auto;
  text-align: center;
}
h1 {
  color: #f64348;
  margin: 1rem auto;
}
footer {
  height: 3rem;
  margin-top: 2rem;
  padding: 1rem 0;
}
a {
  color: #f64348;
}
</style>