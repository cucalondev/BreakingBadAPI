<template>
    <div v-if="show" class="panel panel-default">
      Birthday: {{elementoDetalles.birthday}}
    </div>
    <button @click="show = !show"  class="px-4 py-3 left-60
         bg-blue-600 rounded-md text-white outline-none focus:ring-4 shadow-lg transform active:scale-75 transition-transform">
        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
        </svg>Info</button>
</template>
<script>
export default{
name:'MostrarDetalles',
data:()=>{
  return{
    show:false
  }
},
props:{
elementoDetalles:{
    type:Object,
    }
}
}
</script>
