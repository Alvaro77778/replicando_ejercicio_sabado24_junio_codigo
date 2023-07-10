<template>
    <div id="componenteBienbenida">
        <h2 id="bienbenida">Componente Bienbenida</h2>
        <h3>{{ mensajeEspera }}</h3>
        <div v-if="mostrarDivFormulario">
            
            <button v-on:click.prevent="procesarBienbenida">Ingresar</button>
        </div>
        <p>foolll</p>
        <div id="formulario" v-if="!mostrarDivFormulario">
            <form action="">
                <label for="txtNombre">Nombre:</label>
                <input type="text" id="txtNombre" v-model="nombre"><br>
                <label for="txtApellido">Apellido:</label>
                <input type="text" id="txtApellido" v-model="apellido"><br>
                <input type="button" v-on:click.prevent="mostrarMensajeDeBienbenida" value="enviar">
            </form>
        </div>
        <div id="mensajeBienbenida" v-if="mostrarMensajeBienbenida">
            <p>Mensaje de bienbenida para {{ nombre }}{{  apellido }}</p>
            <button v-on:click.prevent="limpiarInfo">Limpiar</button>
        </div>
        
            
       
        
    </div>
</template>

<script>
    export default{
        name: 'componenteBienbenida',
        props:{
             terminado:{
                type: String,
                required: true
            },
            
        },
        data: function(){
            return{
                nombre: '',
                apellido: '',
                mostrarDivFormulario : true,
                mostrarMensajeBienbenida: false,
            }
        },
        methods:{
            procesarBienbenida: function(){
                this.$emit('iniciar', true);
                
                this.mostrarDivFormulario = false;
                
            },
            mostrarMensajeDeBienbenida: function(){
                this.mostrarMensajeBienbenida = true;
                this.mostrarDivFormulario = true;
                this.$emit('permitirPeliculas', true);
            },
            limpiarInfo: function(){
                this.mostrarMensajeBienbenida = false
            }
        },
        computed: {
            mensajeEspera: function(){
                return this.terminado;
            }
        }
    }
</script>

<style scoped>
    #componenteBienbenida{
        background-color: greenyellow;
    }
</style>