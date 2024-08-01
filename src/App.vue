<template>
<div>
  <NavBar :logo="logo_src" :alt="app_name"/>
  <routerView/>
  <FooterComp/>
</div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import FooterComp from './components/FooterComp.vue';

  export default{
    components: {
      NavBar,
      FooterComp,
      
    },
    data() {
      return {
        logo_src: "./img/logo.png",
        app_name: "Burguer"
      }
    }
  }
</script>

<style>
*{
  font-family: Helvetica, sans-serif;
  padding: 0;
  margin: 0;
}


  .main-container {
    height: 100dvh;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
  }

  h1{
    
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
    text-align: center;  
  }

</style>
