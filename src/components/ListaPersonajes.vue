<template>
  <div v-if="mostrar">
  <ListaFavoritos :ListaFavoritos="personajesFavoritos"  @eliminarFavorito="eliminarFavorito"/>
  <button 
          @click="mostrar=false,limpiarEntrada()"
          class="relative inline-flex items-center justify-center px-10 py-4 overflow-hidden font-mono font-medium tracking-tighter text-white bg-gray-800 rounded-lg group">
          <span class="absolute w-0 h-0 transition-all duration-500 ease-out bg-green-500 rounded-full group-hover:w-56 group-hover:h-56"></span>
          <span class="absolute i)nset-0 w-full h-full -mt-1 rounded-lg opacity-30 bg-gradient-to-b from-transparent via-transparent to-gray-700"></span>
          <span class="relative">Volver</span>
        </button>
  </div>
<div v-else>
  <div>
     <Buscador v-model:entrada="entrada"/><br>
    </div>
        <div id="list-personajes" v-if="personajesFilter && personajesFilter.length">
        <div class="space-y-56 imax-w-sm bg-white rounded-lg border border-lime-900 shadow-md dark:bg-gray-800 dark:border-gray-700" v-for="el of personajesFilter" v-bind:key="el.char_id">
          <div class="p-5" >
            <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{el.name}}   <button 
          @click="añadirFavorito(el.name),mostrar=true" fill="currentColor">
          <svg class="h-4 w-4 text-yellow-500"  fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/>
          </svg>
        </button></h5>
          <img class="rounded-t-lg" :src="el.img" />
      </div>
      </div>
      </div> 
  </div>
  <div v-if="loading">
    <Spinner/>
  </div>
</template>
<script>
import axios from "axios";
import ListaFavoritos from "../components/ListaFavoritos.vue";
import Buscador from "../components/Buscador.vue";
import Spinner from "../components/Spinner.vue";
export default {
  data: () => ({
    entrada:"",
    personajes: [],
    personajesFavoritos:[],
    mostrar:false,
    loading:true
  }),
  components:{
    ListaFavoritos,
    Buscador,
    Spinner
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
        .then((response) => {
          console.log(response);
          this.personajes = response.data;
        })
        .catch((e) => console.log(e))
        .finally(() => this.loading = false);
    },
    añadirFavorito(name){
      if(this.personajesFavoritos.includes(name)){
        return false;
      }
      else{
      this.personajesFavoritos.push(name);
      return true;
      }
    },
    limpiarEntrada(){
      this.entrada=""
    },
    eliminarFavorito(data){
      this.personajesFavoritos = this.personajesFavoritos.filter((el)=> el !== data);
    }
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
</style>
