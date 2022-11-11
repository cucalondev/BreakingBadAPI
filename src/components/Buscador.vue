<template>
   <div class="container">
  <div id="app" class="row">
    <div class="relative flex w-full flex-wrap items-stretch mb-3">
      <input
        :entrada="entrada"
        id="personaje"
        @input="updateProp('entrada', $event)"
        type="text"
        name="personaje"
        class="px-3 py-3 placeholder-slate-300 text-slate-600 relative bg-white rounded text-sm border border-slate-300 outline-none focus:outline-none focus:ring w-full pr-10"
        />
    </div>
  </div>  
</div>
</template>
<script>
export default{
    name:'Buscador',
    emits: ["update:entrada"],
    props:{
            limpiarFiltro:{
                type:Boolean,
                default:false,
            },
            entrada: {
          type: String,
          required: true,
        },
        },
        methods:{
          updateProp(prop, { target: { value } }) {
          this.$emit(`update:${prop}`, value);
},
  }
    };
</script>
<style>
input{
    border:solid 1px;
    border-radius:2px;
}
</style>