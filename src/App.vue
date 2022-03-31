<template>
  <div id="app">
    <Header />
    <Todos />
  </div>
</template>

<script>
import Header from './components/Header.vue'; 
import Todos from './components/Todos.vue'; 

export default {
  components: { Header, Todos },
  name: "App",
  data(){ 
    return {
      name: "App"
    };
  }
  
}
</script>

<style>

</style>