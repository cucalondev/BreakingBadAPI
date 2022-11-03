<template>
  <div>
    <ListaPersonajes />
  </div>
</template>

<script>
import ListaPersonajes from "./components/ListaPersonajes.vue";
export default {
  data: () => ({}),
  components: {
    ListaPersonajes,
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
