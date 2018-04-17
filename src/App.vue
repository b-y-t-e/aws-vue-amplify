<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import store from './vuex/store';
import Vue from "vue";
import VueRouter from "vue-router";
import Amplify, { Auth, Logger } from 'aws-amplify'
import aws_exports from './aws-exports'
import BootstrapVue from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue);
Vue.use(VueRouter);
Amplify.configure(aws_exports)

import SignIn from "./components/SignIn.vue";
import Main from "./components/Main.vue";
import SignUp from "./components/SignUp.vue";

const router = new VueRouter({
  routes: [
    { path: "/", component: SignIn },
    { path: "/Main", component: Main },
    { path: "/signin", component: SignIn },
    { path: "/signup", component: SignUp }
  ]
});

export default {
  store, 
  router,
  name: "app",
  components: {
    SignUp
  },
  data() {
    return {};
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
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
