<template>
  <div id="app">
    <h1>共享单车后台管理</h1>
    <router-view class="content"/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
html, body {
  height: 100%;
  padding: 0;
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  display: flex;
  flex-direction: column;
  background: url(assets/home_bg2.jpg) no-repeat -500px center;
}
#app h1{
	height: 24px;
	line-height: 24px;
}
.content{
	flex: 1;
}
</style>
