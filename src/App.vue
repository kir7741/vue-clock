<template>
  <div id="app">
    <Clock/>
  </div>
</template>

<script>
import Clock from './components/Clock.vue'

export default {
  name: 'app',
  components: {
    Clock
  }
}
</script>

<style lang="scss">
@import './scss/_mixin.scss';
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  background-color: $darkGreen;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}
</style>
