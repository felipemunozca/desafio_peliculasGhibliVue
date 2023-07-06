<template>
    <div class="container col-12">
        <div class="alert alert-primary">
            <p>A continuación hay un listado con los nombres de las películas</p>
        </div>
        <div class="mt-4 mb-5">
            <select @change="obtenerPelicula" v-model="peliculaSeleccionada" class="form-select">
                <option value="" selected>Seleccione una película</option>
                <option v-for="pelicula in listadoPeliculas" :key="pelicula.name" :value="pelicula.name">
                    {{pelicula.name}}
                </option>
            </select>
        </div>
        <div class="row justify-content-center mt-5 mb-4">
            <div v-if="pelicula" class="card p-0" style="width: 25rem">
                <img :src="pelicula.poster" class="card-img-top img-fluid" alt="pelicula.name" />
                <div class="card-body">
                    <h3 class="card-title"><strong>Título original:</strong> {{ pelicula.hepburn }}</h3>
                    <h4 class="card-title"><strong>Título en Inglés:</strong> {{ pelicula.title }}</h4>
                    <p class="card-text"><strong>Descripción:</strong>{{ pelicula.synopsis }}</p>
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item"><strong>Director: </strong>{{ pelicula.director }}</li>
                    <li class="list-group-item"><strong>Duración: </strong>{{ pelicula.runtimeMinutes }} minutos</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
/**
 * Para realizar la petición a la API de studio Ghibli, el desafió pide utilizar axios.
 * Para instalarlo, en la consola del proyecto escribir:
 * npm i axios
 * Luego importar el paquete de axios para poder utilizarlo.
 */
import axios from 'axios';

export default {
    name: 'studio-ghibli-comp',
    // props: {},
    data: function(){
        return {
            listadoPeliculas: [],
            peliculaSeleccionada: "",
            pelicula: null,
        }
    },
    // computed: {},
    methods: {
        async obtenerListaPeliculas() {
            try {
                const resultado = await axios.get(`https://studio-ghibli-films-api.herokuapp.com/api/`);
                // console.log(resultado);

                for (const nombre in resultado.data) {
                    let miPelicula = {
                        name: nombre,
                        data: resultado.data[nombre],
                    };
                    this.listadoPeliculas.push(miPelicula);
                }
            } catch (error) {
                console.log(error);
            }
        },
        obtenerPelicula() {
            if (this.peliculaSeleccionada != '') {
                let seleccion = this.listadoPeliculas.find((element) => element.name === this.peliculaSeleccionada);
                this.pelicula = seleccion.data;
            }
        },
    },
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    created() {
        this.obtenerListaPeliculas();
    }
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    
</style>