<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)

const router = new Router({
  mode: 'history',
  routes: [{
    path: '/',
    component: () => import('./components/Moon.vue')
  }]
})

export default {
  router,
  name: 'App'
}
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap';
  @import url('https://fonts.googleapis.com/css2?family=Oswald&display=swap');
</style>
