<template>
  <div class="products-show">

  <h2>{{ product.name }}</h2>
  <img :src="product.image_url" :alt="product.title">
  <p>{{product.description}}</p>
  <p>{{product.formatted.price}}</p>

  <router-link v-bind:to="'/products/' + product.id + '/edit'">Edit product</router-link><br>

  <router-link to="/">Back to all products</router-link><br>

  <button v-on:click="destroyProduct()">Delete</button>

  </div>
</template>


<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      product: {}
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log(response.data);
      this.product = response.data;
    });
  },
  methods: {
    destroyProduct: function() {
      axios.delete("api/products/" + this.product.id).then(response => {
        console.log("Successfully Removed Product", response.data);
        this.$router.push("/");
      });
    }
  }
};
</script>
