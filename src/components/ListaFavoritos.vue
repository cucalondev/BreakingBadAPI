<template>
    <div>
        <div class="panel panel-default" v-for="el of listaFavoritos" v-bind:key="el.char_id">
          {{
            el.name
          }}
          <img :src="el.img" />
          <br />
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
