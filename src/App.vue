<template>
  <div id="app">
    <moon />
  </div>
</template>

<script>
import Moon from './components/Moon.vue'

export default {
  name: 'App',
  components: {
    Moon
  }
}
</script>

<style lang="scss">
  @import "~bootstrap/scss/bootstrap";
</style>
