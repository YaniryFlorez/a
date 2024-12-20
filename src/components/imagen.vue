<template>
 <div class="container">
  <img v-bind:src="imagen" alt="">
  <h1>{{nombre}}</h1>
</div>


</template>


<script>
export default {
    props:{
   imagen: String,
   nombre: String,

    },

}
</script>


<style>
.container{
    display: flex;
    flex-direction: column;
    align-items: center;

}

</style>