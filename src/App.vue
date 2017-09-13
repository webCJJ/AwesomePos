<template>
  <div id="app">
       <leftNav></leftNav>
       <router-view></router-view>
  </div>
</template>

<script>
import leftNav from "./components/common/leftNav.vue";
export default {
  name: 'app',
  data(){
      return{}
  },
  components:{
     leftNav

  }
}
</script>

<style>
*{margin: 0;padding: 0;}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

</style>
