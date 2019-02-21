<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <h2>All Products</h2>

    <div v-for="product in products">

      <router-link v-bind:to=" '/products/' + product.id">
        <h2>{{ product.name }}</h2>
        <img :src="product.image_url" :alt="product.title">
      </router-link>
      <div>

        <button v-on:click="showProduct(product)">More Info</button>
      </div>
      <div v-if="currentProduct === product">
        <p>{{product.description}}</p>
        <p>{{product.formatted.price}}</p>
        


          
        </div>
      </div>
    </div>
    
  </div>
</template>

<style>
img {
  width: 300px;
}
</style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Welcome to Nerd Stuff!",
      products: [],
      currentProduct: {}
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      this.products = response.data;
    });
  },
  methods: {
    showProduct: function(product) {
      if (this.currentProduct === product) {
        this.currentProduct = {};
      } else {
        this.currentProduct = product;
      }
    }
  }
};
</script>
