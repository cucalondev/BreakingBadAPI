<template>
        <div class="panel panel-default" v-for="el of ListaFavoritos" v-bind:key="el.char_id">
          <img class="w-10 h-15" :src="el.img">
          <p class="left-14 bottom-10">{{el.name}}</p>
          <button 
          @click="eliminarFavorito(el)">
          <svg class="h-
          7 w-7 left-60 bottom-16 text-red-500"  width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">  <path stroke="none" d="M0 0h24v24H0z"/>  <rect x="3" y="4" width="18" height="4" rx="2" />  <path d="M5 8v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2 -2v-10" />  <line x1="10" y1="12" x2="14" y2="12" /></svg>   
        </button>
      </div>
</template>
<script>
export default{
name:'ListaFavoritos',
data: () => ({
    mostrar:false,
  }),
props:{
    ListaFavoritos:{
        type:Array,
    }
},
emits:["eliminarFavorito"],
methods:{
    eliminarFavorito(el){ 
      if (confirm(`¿Estás seguro de eliminar a ${ el.name }?`)) this.$emit("eliminarFavorito", el);
    }
}
}
</script>
