<template>
  <img class="border-none w-60 h-70" id="logoIndex" src="./assets/LogoIndex.png"/>
  <ListaPersonajes textoBoton="Añadir"/>
</template>
<script>
import ListaPersonajes from "@/components/ListaPersonajes.vue";
import ListaFavoritos from "@/components/ListaFavoritos.vue";
export default {
  data: () => ({}),
  components: {
    ListaPersonajes,
    },
};
</script>
