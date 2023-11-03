<template>
  
  
  
  <Navbar :logo="logo_src" :alt="app_name"/>
  
  <router-view/>

  <Footer/>
</template>


<script>

import Navbar from './components/NavBar.vue'
import Footer from './components/Footer.vue'


export default { 

 components:{
  Navbar,
  Footer
 },
 data(){
return{

  logo_src:"/img/rosto.png",
  app_name:"Cadastre a pessoa"
}
   
 }

 }
</script>

<style>


*{

  margin: 0;
  padding: 0;
  box-sizing: border-box; 
  font-family: 'Roboto', sans-serif;
}


.main-container{
  margin: 40px;
  min-height: 600px;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 40px;
  color: #222;
  
}

</style>
