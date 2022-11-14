<template>
  <img class="border-none w-60 h-70" id="logoIndex" src="./assets/LogoIndex.png"/>
  <ListaPersonajes textoBoton="Añadir"/>
  <ListaFavoritos/>
</template>
<script>
import ListaPersonajes from "./components/ListaPersonajes.vue";
import Buscador from "./components/Buscador.vue";
import ListaFavoritos from "./components/ListaFavoritos.vue";
import MostrarFavoritos from "./components/MostrarFavoritos.vue";
export default {
  data: () => ({}),
  components: {
    ListaPersonajes,
    Buscador,
    ListaFavoritos,
    MostrarFavoritos,
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
