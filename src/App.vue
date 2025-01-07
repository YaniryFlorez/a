<template>
  <principalPokemon/>
  
</template>
 
<script>
import Contador from './components/Contador.vue'
import pagPrincipal from './components/pagPrincipal.vue'
import principalPokemon from './components/principalPokemon.vue';

export default {
  name: "App",
  components: {
    Contador,
    pagPrincipal,
    principalPokemon,
    
  },
};
</script>
 
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


