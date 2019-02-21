<template>
  <div class="products-edit">
    <h2>Edit Product</h2>

      <img v-if="status" v-bind:src="'https://http.cat/' + status" alt="">

      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>

    <form v-on:submit.prevent="submit()">
      <div>
        Name: <input type="text" v-model="product.name">
      </div>
      <div>
        Description: <input type="text" v-model="product.description">
      </div>
      <div>
        Price: <input type="text" v-model="product.price">
      </div>
      <div>
        Image Url: <input type="text" v-model="product.image_url">
      </div>

      <div>
        <input type="submit" value="Update">
      </div>

    </form>

  </div>
</template>



<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      product: {},
      errors: [],
      status: ""
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log(response.data);
      this.product = response.data;
    });
  },
  methods: {
    submit: function(product) {
      var productParams = {
        name: this.product.name,
        price: this.product.price,
        description: this.product.description,
        image_url: this.product.image_url
      };
      axios
        .patch("/api/products/" + this.product.id, productParams)
        .then(response => {
          console.log("Success!", response.data);
          this.$router.push("/");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    }
  }
};
</script>
