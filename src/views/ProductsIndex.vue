<template>
  <div class="home">
    <h1>{{ message }}</h1>
      
      <h2>All Products</h2>
      <div class="card-columns">
        <div>
          Search by Name: <input type="text" class="form-control" v-model="nameFilter" list="productNames"><br>
        </div>
          <datalist id="productNames">
            <option v-for="product in products">{{ product.name }}</option>
          </datalist>
            <div>
              <button class="btn btn-primary" v-on:click="setSortAttribute('name')">Sort by Name</button><br>
              <button class="btn btn-primary" v-on:click="setSortAttribute('price')">Sort by Price</button>
            </div>
            <div is="transition-group" name="fade">
              <div v-for="product in orderBy(filterBy(products, nameFilter, 'name', 'price'), sortAttribute, sortAscending)" class="col-md-4"  v-bind:key="product.id">
                <router-link v-bind:to=" '/products/' + product.id">
                  <div class="card" style="width: 18rem;">
                    <img :src="product.image_url" class="card-img-top" alt="product.title">
                      <div class="card-body">
                        <p class="card-text">{{ product.name }}</p>
                      </div>
                  </div>
                </router-link>
              </div>
            </div>
        </div>
  </div>
</template>

<style>
/* Vue.js fade */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

/* Vue.js slide-right */
.slide-right-enter-active {
  transition: all 0.3s ease;
}
.slide-right-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-right-enter,
.slide-right-leave-to {
  transform: translateX(10px);
  opacity: 0;
}

/* Vue.js slide-left */
.slide-left-enter-active {
  transition: all 0.3s ease;
}
.slide-left-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-left-enter,
.slide-left-leave-to {
  transform: translateX(-10px);
  opacity: 0;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to Nerd Stuff!",
      products: [],
      currentProduct: {},
      nameFilter: "",
      sortAttribute: "name",
      sortAscending: 1
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
    },
    setSortAttribute: function(attribute) {
      if (this.sortAttribute === attribute) {
        this.sortAscending = this.sortAscending * -1;
      } else {
        this.sortAscending = 1;
      }
      this.sortAttribute = attribute;
    }
  }
};
</script>
