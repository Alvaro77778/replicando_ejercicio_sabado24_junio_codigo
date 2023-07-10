<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!--
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  -->
  <ComponenteBienbenida
    v-on:iniciar ="consumirApi"
    v-bind:terminado="mensaje"
    v-on:permitirPeliculas="mostrarComponentePeliculas"
  />
<div v-if="mostrarPeliculas">
  <ComponentePeliculas
    v-bind:datosPeliculas="datosConsumidos"
    
  />
</div>
  
</template>

<script>

import ComponenteBienbenida from './components/Bienbenida.vue'
import ComponentePeliculas from './components/Peliculas.vue'


export default {
  name: 'App',
  components: {
    ComponenteBienbenida,
    ComponentePeliculas
  },
  data:function(){
    return{
      mensaje: '',
      datosConsumidos: [],
      mostrarPeliculas: false
    }
  },
  methods:{
    consumirApi: function(flag){
      this.mensaje = 'consumiendo API...';
      if(flag == true){
        let url = 'https://ghibliapi.vercel.app/films/';
        fetch(url)
        .then(response => response.json())
        .then(datosJson =>{
          let timeout = 4000;
          setTimeout(() => {
            this.mensaje = 'se termino de consumir la API';
            console.log(datosJson);
            this.datosConsumidos = datosJson;
            console.log('datos consumidos'+ this.datosConsumidos);
          }, timeout);
        })
        .catch(error =>{
          console.log(error);
        })

      } else{
        console.log('error desconocido')
      }
    },
    mostrarComponentePeliculas: function(autorizacion){
      if(autorizacion == true){
        this.mostrarPeliculas = true;
      }
    }
  }
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
