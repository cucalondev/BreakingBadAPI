<template>
   <div class="container">
  <div id="app" class="row">
    <div class="col-md-8 col-sm-offset-2">
      <input id="input-search" type="text" class="form-control" v-model="entrada" placeholder='Filtrar'>
    </div>
  </div>  
</div>
</template>
<script>
export default{
    name:'Buscador',
    emits:["enviaEntrada"],
    props:{
            limpiarFiltro:{
                type:Boolean,
                default:false,
            }
        },
        data(){
            return{
            entrada:"",
            }
        },
        methods:{
            enviarFiltro(){   
            this.$emit("enviaEntrada", this.entrada);  
            if (this.limpiarFiltro) this.entrada = "";   
            this.$refs.input.focus();
    }
    
  }
    };
</script>
<style>
input{
    border:solid 1px;
    border-radius:2px;
}
</style>