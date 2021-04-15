<template>
<MusicLoad />
</template>

<script>
import MusicLoad from './components/MusicLoad.vue'

export default {
  name: 'App',
  components: {
    MusicLoad
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap');

#app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
