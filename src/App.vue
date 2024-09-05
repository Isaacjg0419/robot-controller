<template>
  <div id="app">
    <RobotGrid />
  </div>
</template>

<script>
import RobotGrid from './components/RobotGrid.vue';

export default {
  name: 'App',
  components: {
    RobotGrid
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 40px;
}
</style>
