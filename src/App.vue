<template>
  <div id="app">

    <LeftNav></LeftNav>

    <div class="main">
      <router-view/>
    </div>
    
  </div>
</template>

<script>
// 引入侧边栏组件
import LeftNav from '@/components/common/LeftNav'
export default {
  name: 'App',
  components:{
    LeftNav
  }
  
}
</script>

<style>
#app {
  font-family: 'Microsoft YaHei','Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.main{
  float: left;
  width: 95%;
  background-color: #eff2f7;
  height: 100%;
  overflow: hidden;

}
</style>
