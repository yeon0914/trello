<template>
  <div id="app">
    <Navbar/> 
    <router-view></router-view>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
export default {
  components: { Navbar },
  name: 'app',
  compoents: {Navbar},
  data () {
    return {
       
    }
  }
}
</script>

<style>
