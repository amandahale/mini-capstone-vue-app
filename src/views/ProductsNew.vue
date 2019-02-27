<template>
  <div class="products-new">
    <h2>Create a Product!</h2>
      
      <img v-if="status" v-bind:src="'https://http.cat/' + status" alt="">

      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>

      <form v-on:submit.prevent="submit()">
        <div>
          Name: <input type="text" class="form-control" v-model="newProductName">
        </div>
        <div>
          Description: <input type="text" class="form-control" v-model="newProductDescription">
        </div>
        <div>
          Price: <input type="text" class="form-control" v-model="newProductPrice">
        </div>
        <div>
          Image Url: <input type="text" class="form-control" v-model="newProductImageUrl">
        </div>
      
        <div>
          <input type="submit" value="Create">
        </div>

      </form>

  </div>
</template>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      newProductName: "",
      newProductDescription: "",
      newProductPrice: "",
      newProductImageUrl: "",
      errors: [],
      status: ""
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      this.products = response.data;
    });
  },
  methods: {
    submit: function() {
      var productParams = {
        name: this.newProductName,
        price: this.newProductPrice,
        description: this.newProductDescription,
        image_url: this.newProductImageUrl
      };
      axios
        .post("api/products", productParams)
        .then(response => {
          console.log("DID IT!", response.data);
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
