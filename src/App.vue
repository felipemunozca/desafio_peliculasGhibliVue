<template>
  <div id="app">
    <Bienvenida @ocultarInformacion="mostrar=false" @mostrarInformacion="mostrar=true"/>
    <!--  
      Para crear una validación correcta del segundo componente de la pagina, en vez de utilizarlo directamente
      en el archivo "App", se declara e inicia en el archivo "Bienvenida", de esta manera pasa a ser su hijo y
      se puede validar si mostrar o no la segunda sección.
    -->
    <!-- <Peliculas v-if="mostrar"/> -->
  </div>
</template>

<script>
import Bienvenida from '@/components/Bienvenida.vue';
/* import Peliculas from '@/components/Peliculas.vue'; */

export default {
  name: 'App',
  data(){
    return{
      mostrar: false,
    }
  },
  components: {
    Bienvenida,
    /* Peliculas, */
  },
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
}
</style>
