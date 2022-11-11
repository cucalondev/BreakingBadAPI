<template>
    <div>
        <div class="panel panel-default" v-for="el of ListaFavoritos" v-bind:key="el.char_id">
          {{el}}
          <button 
          @click="eliminarFavorito(el)">
          <svg class="h-8 w-8 text-red-500"  width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">  <path stroke="none" d="M0 0h24v24H0z"/>  <rect x="3" y="4" width="18" height="4" rx="2" />  <path d="M5 8v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2 -2v-10" />  <line x1="10" y1="12" x2="14" y2="12" /></svg>   
        </button>
      </div>
    </div>
</template>
<script>
export default{
name:'ListaFavoritos',
props:{
    ListaFavoritos:{
        type:Array,
    }
},
emits:["eliminarFavorito"],
methods:{
    eliminarFavorito(name){ 
      if (confirm(`¿Estás seguro de eliminar a ${ name }?`)) this.$emit("eliminarFavorito", name);
    }
}
}
</script>
