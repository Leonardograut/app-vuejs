<template>

<div class="mensagem-container">

<h2>{{ msg }}</h2>


</div>

</template>


<script>
  export default {

name: "Mensagem",

props:{
    msg:String
}

  }

</script>


<style scoped>

.mensagem-container{
    color: wheat;
    background-color: red;
    border: 2px solid rgb(209, 202, 202);
    padding: 10px;
    border-radius: 5px;
    max-width: 400px;
    margin: 30px auto;
}

</style>