<template>
    <label>Filtar por nombre o apellido:</label>
    <br>
    <input
        ref="input"
        v-model="entrada"
        type="text"
        placeholder="Filtar"
        @keydown.enter="enviarFiltro"
      />
</template>
<script>
export default{
    name:'Buscador',
    emits: ["enviaEntrada"],
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