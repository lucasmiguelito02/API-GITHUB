<script setup>
import { reactive, ref, computed, onMounted, onUpdated, onUnmounted } from 'vue';
import Form from './Form.vue';
import UserInfo from './UserInfo.vue';
import Repository from './Repository.vue';


const searchInput = ref('')

const state = reactive({
  login: '',
  name: '',
  bio: '',
  company: '',
  avatar_url: '',
  repos:  [],
  searchInput: ''
})

async function fetchGithubUser(username) {
  ev.preventDefault()
  const res = await fetch(`https://api.github.com/users/${username}`)
  const { login, name, bio, company, avatar_url } = await res.json()

  state.login = login
  state.name = name
  state.bio = bio
  state.company = company
  state.avatar_url = avatar_url
  state.repos = []

	fetchUserRepositories()
}

async function fetchUserRepositories() {
  const res = await fetch(`https://api.github.com/users/${state.login}/repos`)
  const repos = await res.json()
  state.repos = repos
}

const reposCountMessage = computed(() => {
  return state.repos.length > 0
    ? `${state.name} possui ${state.repos.length} repositórios públicos.`
    : `${state.name} não possui nenhum repositório público.`
})

onMounted(() => {
  console.log("O componente foi montado.")
})

onUpdated(() => {
  console.log("O componente foi atualizado.")
})

onUnmounted(() => {
  console.log("O componente foi desmontado.")
})

</script>

<template>
	<h1>GitHub User Data</h1>
  <p>Pesquisando por: <strong>https://api.github.com/users/{{ searchInput }}</strong></p>
  <Form @form-submit="fetchGithubUser" v-model="searchInput" />
    <UserInfo v-if="state.login" :login="state.login" :name="state.name" :company="state.company" :bio="state.bio" :avatar_url="state.avatar_url" />

    <section v-if="state.repos.length > 0">
      <h2>{{ reposCountMessage }}</h2>
        <Repository v-for="repo of state.repos" :full_name="repo.full_name" :description="repo.description" :html_url="repo.html_url" /> 
    </section>
</template>

<style scoped>
h1 {
  color:  #f64348;
}
</style>