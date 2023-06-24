<template>
    <div id="Peliculas">
        
        <h1>Studio Ghibli Films</h1>

        <label for="peliculas">Elija pelicula:</label><br>
        <select name="peliculas" id="peliculas" v-on:change="mostrarDatosPeliculas()" >
            <option  v-for="(pelicula,index) in datosPeliculas" :key="index" :value="index" >{{pelicula.title}} </option> 
        </select><br><br>
        <div class="container" id="cardInfo" >
            <div class="card" v-if="mostrarCardIfo">
                 <img v-bind:src="rutaImagen" v-bind:alt="nombreIngles" class="imagen"> 
                <div class="card-body">
                    <h2 class="card-text">Titulo: {{ titulo }}</h2>
                    <h2 class="card-text">Titulo Idioma: {{ nombreOriginal }}</h2>
                    <h3 class="card-title">Titulo Ingles: {{ nombreIngles }}</h3><br>  
                    <p><strong>Descripción:</strong>  {{ descripcionPelicula }}</p>
                    <h3 id="parrafoDirector">Director: {{ directorPelicula }}</h3>
                    <h5 id="parrafoDuracion">Duración: {{ duracionPelicula }} min</h5>
                    <h5 id="parrafoAnio">Año lanzamiento: {{ produccion }}</h5>
                   
                </div>
            </div>
        </div>

    </div>
</template>
<script>
export default{
    name:'Peliculas',
    props:{
        datosPeliculas:{
            type: Array,
            required: true,
        },
    },
    data: function(){
        return{
            mostrarCardIfo:'',
            opcionPelicula:0,
            nombreOriginal: '',
            titulo:'',
            nombreIngles:'',
            descripcionPelicula:'',
            directorPelicula:'',
            duracionPelicula:'',
            produccion:'',
            rutaImagen:'',

        }
    },
    methods:{
        mostrarDatosPeliculas:function(){
            console.log('MostrarDatosPeliculas');
            this.opcionPelicula = Number(document.getElementById('peliculas').value);
            console.log(this.opcionPelicula);
            this.titulo= this.datosPeliculas[this.opcionPelicula].title;
            this.nombreOriginal = this.datosPeliculas[this.opcionPelicula].original_title;
            this.nombreIngles = this.datosPeliculas[this.opcionPelicula].original_title_romanised;
            this.descripcionPelicula = this.datosPeliculas[this.opcionPelicula].description;
            this.directorPelicula = this.datosPeliculas[this.opcionPelicula].director;
            this.duracionPelicula = this.datosPeliculas[this.opcionPelicula].running_time;
            this.produccion= this.datosPeliculas[this.opcionPelicula].release_date;
            this.rutaImagen = this.datosPeliculas[this.opcionPelicula].image;
            this.mostrarCardIfo= true;
        },
    }
}
</script>

<style scoped>
.card-body{
    border:1px solid grey;
}
#parrafoDirector{
    border: 0.5px solid grey;
}
#parrafoDuracion{
    border: 0.5px solid grey;
}
#parrafoAnio{
    border: 0.5px solid grey;
}

</style>