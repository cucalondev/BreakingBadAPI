<template>
    <div class="panel panel-default" v-for="el of ListaDetalles" v-bind:key="el.char_id">
      {{el.name}}
  </div>
</template>
<script>
export default{
name:'MostrarDetalles',
props:{
ListaDetalles:{
    type:Array,
    }
}
}
</script>
