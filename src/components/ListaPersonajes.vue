<template>
  <!--Mostrar favoritos-->
  <div v-if="mostrar && contador>0">
    <div v-if="show"><AlertAñadido/></div>
  <ListaFavoritos :ListaFavoritos="personajesFavoritos" @eliminarFavorito="eliminarFavorito"/>
    <!--Volver a la ventana principal-->
    <button 
          @click="mostrar=false,limpiarEntrada()"
          class="relative inline-flex items-center justify-center px-10 py-4 overflow-hidden font-mono font-medium tracking-tighter text-white bg-gray-800 rounded-lg group">
          <span class="absolute w-0 h-0 transition-all duration-500 ease-out bg-green-500 rounded-full group-hover:w-56 group-hover:h-56"></span>
          <span class="absolute i)nset-0 w-full h-full -mt-1 rounded-lg opacity-30 bg-gradient-to-b from-transparent via-transparent to-gray-700"></span>
          <span class="relative">Volver</span>
        </button>
  </div>
  <!--Mostrar ventana principal-->
<div v-else>
  <br><br>
  <div>
    <!---Botón favoritos-->
    <div class="flex border-b-2 border-grey-dark  rounded-lg overflow-hidden">
      <button @click="mostrar=true"
        class="inline-flex text-white bg-lime-900 items-center shadow-border bg-blue hover:bg-blue-dark text-sm py-3 px-6 font-sans tracking-wide font-bold">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" viewBox="0 0 20 20" fill="currentColor">
          <path
            d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
        </svg>
        Favoritos {{this.contador}}
      </button>
    </div>
  <div>
    <!--Buscador-->
     <Buscador v-model:entrada="entrada"/><br>
    </div>
    <!--Mostrar personajes-->
        <div id="list-personajes" v-if="personajesFilter && personajesFilter.length">
        <div class="relative my-5 imax-w-sm bg-white rounded-lg border border-lime-900 shadow-md dark:bg-gray-800 dark:border-lime-900" v-for="el of personajesFilter" v-bind:key="el.char_id">
          <div class="p-5" >
            <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{el.name}}   <button id="btn"
          @click="setShow(),añadirFavorito(el)?mostrar=true:mostrar=false">
          <svg class="h-8i w-8 text-yellow-500" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/>
          </svg>
        </button></h5>
      <img class="rounded-t-lg" :src="el.img" /><br>
      <MostrarDetalles :personajeDetalles="el"/>
        </div>
      </div>
      </div>
      </div> 
      <!--Spinner-->
      <div v-if="loading">
    <Spinner/>
  </div>
  </div>
</template>
<script>
import axios from "axios";
import ListaFavoritos from "../components/ListaFavoritos.vue";
import Buscador from "../components/Buscador.vue";
import Spinner from "../components/Spinner.vue";
import MostrarDetalles from "../components/MostrarDetalles.vue";
import AlertAñadido from "../components/AlertAñadido.vue";
export default {
  data: () => ({
    entrada:"",
    personajes: [],
    personajesFavoritos:[],
    mostrar:false,
    loading:true,
    contador:0,
    mostrarDetalles:false,
    show:false,
    unshow:false,
  }),
  components:{
    ListaFavoritos,
    Buscador,
    Spinner,
    MostrarDetalles,
    AlertAñadido,
    },
  props: {
    textoBoton:{
      type: String
    }},
  mounted() {
    this.getTodos();
  },
  methods: {
    getTodos() {
      axios
        .get("https://www.breakingbadapi.com/api/characters/")
        .then((personajes) => {
          console.log(personajes);
          this.personajes = personajes.data;
        })
        .catch((e) => console.log(e))
        .finally(() => this.loading = false);
    },
    añadirFavorito(name){
      if(this.personajesFavoritos.includes(name)){
        alert("El personaje ya está añadido a favoritos");
        return false;
      }
      else{
      this.personajesFavoritos.push(name);
      this.contador++;
      return true;
      }
    },
    limpiarEntrada(){
      this.entrada=""
    },
    setShow() {
      this.show = true;
      setTimeout(() => {
        this.show = false;
      }, 2000);
    },
    eliminarFavorito(data){
      this.personajesFavoritos = this.personajesFavoritos.filter((el)=> el !== data);
      this.contador--;
      this.unshow = true;
      setTimeout(() => {
        this.unshow = false;
      }, 100);
    },
    
  },
  computed: {
     personajesFilter: function() {
      let texto = this.entrada;
       return this.personajes.filter(function(el) {
         return el.name.toLowerCase().indexOf(texto.toLowerCase()) !== -1;
       });
     }
  },
};
</script>
<style>
img {
  height: 150px;
  width: 100px;
  object-fit: cover;
  margin-right: 10px;
  border: 2px solid black;
  border-radius: 3px;
}
#btn:hover{
  fill:currentColor;
}
</style>
