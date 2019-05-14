<template>
  <div id="app">
    <router-view/>
  </div>
</template>
<script>
import home from './views/Home'
export default {
  data () {
    return {
    }
  },
  components: {
    vhome: home
  }
}
</script>
<style lang="less">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
html,
body {
  height: 100%;
}
ul,
li {
  list-style: none;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  overflow: hidden;
}
</style>
