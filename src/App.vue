<template>
  <div id="flashMessage" v-if="GStore.flashMessage">
    {{ GStore.flashMessage }}
  </div>
  <div id="nav">
    <router-link :to="{ name: 'EventList', query: { perPage: '3' } }"
      >Home</router-link
    >
    |
    <router-link :to="{ name: 'About' }">About</router-link>
  </div>

  <!-- new element -->
  <router-view />
</template>
<script>
export default {
  inject: ['GStore']
}
</script>
<style>
@keyframes yellowfade {
  from {
    background: #2c3e89
  }
  to {
    background: transparent;
  }
}

#flashMessage {
  animation-name: yellowfade;
  animation-duration: 5s;
  color: wheat;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
h4 {
  font-size: 20px;
}
</style>
