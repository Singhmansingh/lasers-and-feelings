<template>
  <GameScreen/>
</template>

<script>
import GameScreen from './components/GameScreen.vue'

export default {
  name: 'App',
  components: {
    GameScreen
  }
}
</script>

<style>
@font-face {
  font-family: "Title";
  src: url("./assets/fonts/lazenby-computer.liquid.ttf");
}
@font-face {
  font-family: "Name";
  src: url("./assets/fonts/Enter-The-Grid.ttf");
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  display:flex;
  background-color: #cae4ff;

   background-image: url('./assets/circuit_board.jpg');
    background-blend-mode: screen;
    background-position: center;

}
body {
  margin:0;
  width: 100vw;
  height: 100vh;
  background-color: #2c3e50;
  overflow:hidden;
}
</style>
