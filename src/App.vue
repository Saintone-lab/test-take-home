<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-sm-12 col-lg-3">
        <SideBar/>
      </div>
      <div class="col-sm-12 col-lg-9"> <router-view/> </div>
    </div>
  </div>
</template>


<script>
  import 'bootstrap/dist/css/bootstrap.css'
  import SideBar from './components/SideBar.vue'
  export default {
    name: 'app',
    components: {
      SideBar
    }
  }
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
@import "~@flaticon/flaticon-uicons/css/all/all";
</style>
