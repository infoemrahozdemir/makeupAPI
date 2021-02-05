<template>
<!-- Search Area  -->
  <div class="row">
						<div class="column">
                <form @submit.prevent="SearchProducts()" class="row row-center">
                  <input type="text" placeholder="Nail polish, Blush, Lipstick and more..." v-model="search">
                  <input type="submit" value="Search" class="button-primary">
                </form>
            </div>
  </div>
  <!-- Search Results Listing  -->
  <div class="product-row">
            <div  v-for="product in products" :key="product.id"  class="product product-column">   
                    <router-link :to="'/product/'+product.id" class="product-link">
                          <div class="product-image">
                              <img :src="product.image_link" :alt="product.name"> 
                          </div>
                          <div class="detail">
                              <h3>{{product.name}}</h3>
                              <p>{{product.price_sign}}{{product.price}}</p>
                          </div>
                    </router-link> 
            </div>
  </div>
</template>

<script>
import{ref} from 'vue';

export default {
      setup()
      {
        /*
        Get value from the search field 
        make an api call
        push data in products variable
        reset the form
        return values
        */
            const search = ref("");
            const products = ref([]);
            const SearchProducts = () => {
                if(search.value != ""){
                    fetch(`http://makeup-api.herokuapp.com/api/v1/products.json?product_type=${search.value}`)
                    .then(response => response.json())
                    .then(data=>{
                      products.value = data;
                      search.value = ""; 
                    })
                }
            }

    return{
              search,
              products,
              SearchProducts
          }
    }
}
</script>