<template>
    <button @click="mostrarFavoritos=true">Favoritos</button>
    <div v-if="mostrarFavoritos">
        <ListaFavoritos/>
    </div>
</template>
<script>
import ListaFavoritos from "../components/ListaFavoritos.vue";
export default {
  data: () => ({
    mostrarFavoritos:false,
  }),
  components:{
    ListaFavoritos,
  }
}

</script>
