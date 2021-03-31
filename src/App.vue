<template>
  <FramePicker />
</template>

<script>
import FramePicker from './components/FramePicker'


export default { 
  name: 'App',
  components: {
    FramePicker,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  margin-right: 80px;
  margin-left: 80px;
}

</style>
