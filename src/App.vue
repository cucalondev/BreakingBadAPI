<template>
  <div>
    <div class="grid place-items-center">
    <img class="w-60 h-70" id="logoIndex" src="./assets/LogoIndex.png"/>
  </div>
    <ListaPersonajes textoBoton="Añadir"/>
    <ListaFavoritos/>
  </div>
</template>
<script>
import ListaPersonajes from "./components/ListaPersonajes.vue";
import Buscador from "./components/Buscador.vue";
import ListaFavoritos from "./components/ListaFavoritos.vue";
export default {
  data: () => ({}),
  components: {
    ListaPersonajes,
    Buscador,
    ListaFavoritos,
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
#logoIndex{
  border:none;
}
p{
 color:blue;
 font-size:20px;
 text-align:center;
}
template{
  background-color:black;
}
</style>
