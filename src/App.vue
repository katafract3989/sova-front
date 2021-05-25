<template>
  <div id="app">
    <div id="nav">
      <router-link to="/"><b-icon-camera-video />Camers</router-link>
      |
      <router-link to="/login">Log in</router-link>
    </div>
    <router-view />
  </div>
</template>
<script>
import Vue from "vue";
import { IconsPlugin } from "bootstrap-vue";
Vue.use(IconsPlugin);
export default {
  methods: {},
};
</script>
<style lang="scss">
body {
  background: url("https://images.pexels.com/photos/948811/pexels-photo-948811.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940");
  background-repeat: no-repeat;
  background-size: cover;
}
@media (max-width: 1200px) {
  body {
    background: #fff;
  }
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

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #ee2f0d;
    }
  }
  svg {
    fill: #ee2f0d;
    margin-right: 5px;
  }
  img {
    position: fixed;
    left: 30px;
  }
}
</style>
