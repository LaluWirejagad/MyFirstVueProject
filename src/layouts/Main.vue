<template id="App">
  <h1>Vue Project</h1>
  <ul>
    <li v-for="key in routeData" v-bind:key="key">
      <v-link v-if="key.path !== this.$root.currentRoute" :href="key.path">{{key.label}}</v-link>
      <p  v-else>{{key.label}}</p>
    </li>
  </ul>
  <slot></slot>
  <img alt="Vue logo" src="../assets/logo.png">
</template>

<script>
import VLink from '../components/VLink.vue'

export default {
  components: {
    VLink
  },
  data() {
    return {
      routeData: [
        {path:"/",label:"Calculator"},
        {path:"/about",label:"Local Save"},
        {path:"/app",label:"API Test"},
        ]
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
