<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App 333" s1="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" :my-message="msg"/> -->
    <hello-world msg="Welcome to Your Vue.js App 555" s1="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" :my-message="msg"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data () {
    return {
      msg : '안녕하세요 !!'
    }

  },
  components: {
    HelloWorld

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
