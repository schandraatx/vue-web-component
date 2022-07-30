<template>
    <GithubUsers></GithubUsers>
</template>

<script>
import GithubUsers from './components/UsersList.ce.vue'

export default {
  name: 'App',
  components: {
    GithubUsers
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
