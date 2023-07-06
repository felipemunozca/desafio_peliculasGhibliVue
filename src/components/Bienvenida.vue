<template>
    <div class="container">
        <button @click="crearUsuario" class="btn btn-success">Ingresar Datos</button>
        <!--  
            Se crea una validación para que las variables nombre y apellido no tengan ni un valor vació, ni un valor nulo.
        -->
        <div v-if="nombre!='' && apellido!='' && nombre!=null && apellido!=null">
            <div class="col-8 mx-auto mt-4 border border-danger">
                <h2>Bienvenid@ {{nombreCompleto}}</h2>
                <p>Aquí podrás encontrar información de películas de anime del studio Ghibli</p>
                <button @click="limpiarPagina" class="btn btn-warning mt-4 mb-3 col-10">Limpiar información</button>
            </div>
            <!--  
                Si todas las condiciones del v-if se cumplen, se imprime el componente "Películas" por lo que pasa a ser hijo
                de este componente "Bienvenida".
            -->
            <div class="mt-5">
                <Peliculas/>
            </div>
        </div>
    </div>
</template>

<script>
import Peliculas from '@/components/Peliculas.vue';

export default {
    name: 'bienvenida-comp',
    // props: {},
    data: function(){
        return {
            nombre: "",
            apellido: "",
        };
    },
    computed: {
        nombreCompleto() {
            return `${this.nombre} ${this.apellido}`;
        },
    },
    methods: {
        crearUsuario() {
            this.nombre = prompt('Ingrese su nombre:');
            this.apellido = prompt('Ingrese su apellido');
            this.$emit('mostrarInformacion');
        },
        limpiarPagina() {
            this.nombre = "";
            this.apellido = "";
            this.$emit("ocultarInformacion");
        },
    },
    // watch: {},
    components: {
        Peliculas,
    },
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    
</style>