<template>
  <div id="appVue">
  <Ingreso
    v-on:iniciar="consumirAPI"
    v-on:permitirPeliculas="mostrarComponentePeliculas"
    v-bind:terminado="mensaje"
  />
  <div v-if="mostrarPeliculas">
        <Peliculas 
        v-bind:datosPeliculas="datosConsumidos"
      />
  </div>

  </div>
  <footer id="mi_footer" class="mifooter">
      <b> <p class="mifooter__eltextoreservado">TODOS LOS DERECHOS RESERVADOS ® J.U.</p> <!--&#174 codigo acci--> </b>    
  </footer>
</template>

<script>
import Ingreso from './components/Ingreso.vue';
import Peliculas from './components/Peliculas.vue';

export default {
 
  name: 'App',
  components: {

    Ingreso,
    Peliculas
  },
  data:function(){
    return{
        mensaje:'',
        datosConsumidos:[],
        mostrarPeliculas: false,
    }
  },
  methods:{
    consumirAPI: function(flag){
      this.mensaje='...Consumiendo API, por favor espere';
      if(flag==true){
        let url='https://ghibliapi.vercel.app/films';
        fetch(url)
        .then(respuesta=> respuesta.json())
              .then(datosJson =>{

                let timeout= 1500;
                setTimeout(() => {
                  this.mensaje = 'Se terminó de consumir la API después de 10 segundos';
                  this.datosConsumidos = datosJson;
                  console.log(datosJson);
                }, timeout);
                

              })
        .catch(error=> console.log('Error consumiendo API', error));
      }else{
        console.log('Error desconocido');
      }

    },
    mostrarComponentePeliculas:function(autorizacion){
      if(autorizacion== true){
        this.mostrarPeliculas = true;
      }
    },

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
  margin-top: 40px;
 
}

.container{
  width: 40%;
}
.mifooter {   
    border: 2px solid blueviolet;
    background-image: linear-gradient(90deg, #f387ea 0%, #acf570 100%);
  }
  
  .mifooter__eltextoreservado {
    font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
    color: rgb(8, 8, 8);
  }

</style>
