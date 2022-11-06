<template>
  <div>
    <p>The Breaking Bad</p>
    <label>Buscar por nombre:</label>
    <ListaPersonajes textoBoton="Añadir"/>
  </div>
</template>
<script>
import ListaPersonajes from "./components/ListaPersonajes.vue";
import Buscador from "./components/Buscador.vue";
export default {
  data: () => ({}),
  components: {
    ListaPersonajes,
    Buscador,
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
p{
 color:blue;
 font-size:20px;
 text-align:center;
}
template{
  background-color:black;
}
</style>
