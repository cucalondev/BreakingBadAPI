<template>
  <div>
    <div class="container">
  <div id="app" class="row">
    <div class="col-md-8 col-sm-offset-2">
      <Buscador @enviaEntrada="recibePersonaje" v-model="this.entrada"/>
    </div>
  </div>  
</div>
        <div id="list-personajes" v-if="personajesFilter && personajesFilter.length">
        <div class="panel panel-default" v-for="el of personajesFilter" v-bind:key="el.char_id">
          {{
            el.name
          }}
          <img :src="el.img" />
          <button 
          @click="añadirFavorito(el.name)" 
          class="relative inline-flex items-center justify-center px-10 py-4 overflow-hidden font-mono font-medium tracking-tighter text-white bg-gray-800 rounded-lg group">
          <span class="absolute w-0 h-0 transition-all duration-500 ease-out bg-green-500 rounded-full group-hover:w-56 group-hover:h-56"></span>
          <span class="absolute i)nset-0 w-full h-full -mt-1 rounded-lg opacity-30 bg-gradient-to-b from-transparent via-transparent to-gray-700"></span>
          <span class="relative">{{this.textoBoton}}</span>
        </button>
          <br />
      </div>
      </div>
  </div>
  <ListaFavoritos :ListaFavoritos="personajesFavoritos"/>
</template>
<script>
import axios from "axios";
import ListaFavoritos from "../components/ListaFavoritos.vue";
import Buscador from "../components/Buscador.vue";
export default {
  data: () => ({
    entrada:"",
    personajes: [],
    personajesFavoritos:[]
  }),
  components:{
    ListaFavoritos,
    Buscador,
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
        .catch((e) => console.log(e));
    },
    añadirFavorito(name){
      this.personajesFavoritos.push(name);
    },
    recibePersonaje(data){
        this.entrada=data;
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
