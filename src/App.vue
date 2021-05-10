<template>
  <div id="app">
    <draggable />
  </div>
</template>

<script>
/**
 * https://www.kirupa.com/html5/drag.htm
 * Kirupa's vanilla js draggable example roughly adapted for vue 2
 */
import Draggable from './components/Draggable.vue'

export default {
	name: 'App',
	components: {
		Draggable,
	},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
