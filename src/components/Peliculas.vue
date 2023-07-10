<template>
    <div id="componentePeliculas">


        <label for="peliculas">Elija Película:</label>
        <select name="peliculas" id="peliculas" v-on:change="mostrarDatosPeliculas()">
            <option v-for="(pelicula, index) in datosPeliculas"
             v-bind:key="index"
             v-bind:value="index"
            >
                {{ pelicula.title }}
            </option>
        </select>

      
                <div>
            <img v-bind:src="rutaImagen" v-bind:alt="nombreIngles">
            <h3>Titulo Original: {{ nombreOriginal }}</h3>
            <h4>Titulo Inglés: {{ nombreIngles }} </h4>
            <p>Descripción:  {{ descripcionPelicula }}</p>
            <p>Director: {{  directorPelicula }}</p>
            <p>Duración: {{  duracionPelicula }}</p>

        </div>
    </div>
</template>

<script>
    export default{
        name: 'componentePeliculas',
        props: {
            datosPeliculas: {
                type: Array,
                required: true,
            }
        },
    
        data: function(){
            return{
                opcionPelicula:0,
                nombreOriginal: '',
                nombreIngles:'',
                descripcionPelicula:'',
                directorPelicula:'',
                duracionPelicula:'',
                rutaImagen:'',
            }
        },
        methods: {
                mostrarDatosPeliculas:function(){
                    console.log('MostrarDatosPeliculas');
                    this.opcionPelicula = Number(document.getElementById('peliculas').value);
                    console.log('id pelicula seleccionada, ' + this.opcionPelicula);
                    this.nombreOriginal = this.datosPeliculas[this.opcionPelicula].original_title_romanised;
                    this.nombreIngles = this.datosPeliculas[this.opcionPelicula].title;
                    this.descripcionPelicula = this.datosPeliculas[this.opcionPelicula].description;
                    this.directorPelicula = this.datosPeliculas[this.opcionPelicula].director;
                    this.duracionPelicula = this.datosPeliculas[this.opcionPelicula].running_time;
                    this.rutaImagen = this.datosPeliculas[this.opcionPelicula].image;
                },
        }
    }
</script>

<style scoped>
    #componentePeliculas{
        background-color:darkolivegreen;
        color: wheat;
    }
</style>