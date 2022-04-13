<template>
  <Main />
  <!-- <hello-world/> -->
</template>

<script>
import Main from './pages/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #131516;
  height: 100%;
}
html,body{
	height: 100%;
  margin: 0px;
}
.content {
  background-image: url('http://seopic.699pic.com/photo/50055/5642.jpg_wh1200.jpg');//网络图片
  height: 100%;
  background-size: 100% 100%;
}
</style>