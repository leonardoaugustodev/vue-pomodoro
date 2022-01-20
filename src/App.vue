<template>
  <Pomodoro />
</template>

<script>
import Pomodoro from './components/Pomodoro.vue'

export default {
  name: 'App',
  components: {
    Pomodoro
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Fredoka+One&display=swap');

body{
  margin: 0;
  padding: 0;
  box-sizing: content-box;
}

#app {
  font-family: 'Fredoka One', cursive;
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FFF;
  background: #1e2140;
  height: 100vh;
  position: relative;

}
</style>
