<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("/products.json").then((response) => {
        this.products = response.data;
        console.log("All products:", this.products);
      });
    },
  },
};
</script>

<template>
  <div v-for="product in products" v-bind:key="product.id">
    <h3>
      <router-link :to="`/products/${product.id}`">{{ product.name }}</router-link>
    </h3>
    <p>${{ product.price }}</p>
    <img v-bind:src="product.image_url" :alt="product.name" />
  </div>
</template>
