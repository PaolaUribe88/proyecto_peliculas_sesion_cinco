<template>
    <div id="Ingreso">
            <div id="divIngresar" v-if="mostrasDivIngresar">
                <button class="btn btn-success" v-on:click.prevent="ingresarBienvenida">INGRESAR DATOS</button>
            </div><br><br>
            
            <div class="container" v-if="!mostrasDivIngresar" id="divFormulario">
                <form class="form-control">
                    <label for="txtNombre">Nombre</label><br>
                    <input type="text" id="txtNombre" v-model="nombre" placeholder="Ingrese Nombre"><br>
                    <label for="txtApellido">Apellido</label><br>
                    <input type="text" id="txtApellido" v-model="apellido" placeholder="Ingrese Apellido"><br>
                    <input type="submit" id="btnEnviar" v-on:click.prevent="presentarMensajeBienvenida" value="Enviar">
                
                </form><br>
            </div>
            <div id="mensajeBienvenida" v-if="mostrarMensajeBienvenida">
                <form class="container" id="cajaBienvenida">
                    <p id="parrafoSaludo"> Bienvenid@ {{ nombre}} {{ apellido }}</p>
                    <p>Aqui podras encontrar infiormacion de peliculas de anime de Studio Ghibií</p>
                    <button v-on:click="limpiarInfo" id="limpiarInfo">Limpiar Informacion</button>
                    
                </form><br><br>
                
            </div>
    
       
    </div>
</template>
<script>
export default{
    name:'Ingreso',
    props:{
        terminado:{
            type: String,
            required:true,
        },

    }, 
    data:function(){
        return{
            mostrasDivIngresar: true,
            mostrarMensajeBienvenida: false,
            nombre: '',
            apellido:'',
        }
    },
    methods:{
        ingresarBienvenida:function(){
            this.$emit('iniciar', true);
            this.mostrasDivIngresar = false;
        },
        presentarMensajeBienvenida: function(){
            // console.log('presentar bienvenida');
            this.mostrarMensajeBienvenida = true;
            this.mostrasDivIngresar = true;
            this.$emit('permitirPeliculas', true);
        },
        limpiarInfo:function(){
            this.mostrarMensajeBienvenida = false;
        },
    },
    computed:{
        mensajeEspera:function(){
            return this.terminado;
        },
    }
}
</script>

<style scoped>
#Ingreso{
   background-color:white;
}
#limpiarInfo{
    background-color: rgb(249, 225, 8);
}
#cajaBienvenida{
    border: 1px solid lightgrey;
}
</style>