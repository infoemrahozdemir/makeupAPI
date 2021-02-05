<template>
<!-- Product Details Listing  -->
<div class="row">
    <div class="column">
      <img :src="product.image_link" :alt="product.name"> 
    </div>
    <div class="column">
      <h2>{{product.name}}</h2> 
      <h3>Brand:</h3><p> {{product.brand}}</p>
      <h3>Description:</h3><p> {{product.description}}</p>
      <a :href="product.product_link" target="_blank" class="button button-outline">Buy Now: {{product.price_sign}}{{product.price}}</a>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
export default {
setup(){
        /*
        Get value from the route params (id)
        make an api call
        push data in product variable
        return values
        */  
        const product = ref({});
        const route = useRoute();

  onBeforeMount( () =>{
          fetch('https://makeup-api.herokuapp.com/api/v1/products/'+route.params.id+'.json')
          .then(response => response.json())
          .then(data=>{
            product.value = data;});
    });
            
  return {
    product
    }
  } 
} 
</script>
