<template>
  <div>
    <div class="main-container">
      <h1>Monte seu hamburguer</h1>
      <BurguerForm />
      
    </div>
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import BurguerForm from '@/components/BurguerForm.vue';

export default {
  name: "home",
  components:{
    Banner,
    BurguerForm
  } 
}
</script>

<style>
  
</style>


