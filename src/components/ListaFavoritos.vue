<template>
    <div>
        <div class="panel panel-default" v-for="el of ListaFavoritos" v-bind:key="el.char_id">
          {{el}}
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
}
}
</script>
