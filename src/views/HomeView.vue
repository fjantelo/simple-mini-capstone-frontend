<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      newProductParams: {},
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        this.products = response.data;
        console.log("All products:", this.products);
      });
    },
    createProduct: function () {
      axios.post("http://localhost:3000/products.json", this.newProductParams).then((response) => {
        console.log("Product created", response.data).catch((error) => console.log(error.response));
        this.products.push(response.data);
      });
      this.newProductParams = {};
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>New Product</h2>
    <div>
      Name:
      <input type="text" v-model="newProductParams.name" />
      Description:
      <input type="text" v-model="newProductParams.description" />
      Price:
      <input type="text" v-model="newProductParams.price" />
      Image URL:
      <input type="text" v-model="newProductParams.image_url" />
    </div>
    <button v-on:click="createProduct()">Create Product</button>
    <div v-for="product in products" v-bind:key="product.id">
      <h3>{{ product.name }}</h3>
      <p>${{ product.price }}</p>
      <img v-bind:src="product.image_url" :alt="product.name" />
    </div>
  </div>
</template>

<style>
.bluetext {
  color: blue;
}
</style>
