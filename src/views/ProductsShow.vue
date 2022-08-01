<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: {},
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id + ".json").then((response) => {
      this.product = response.data;
    });
  },
  methods: {
    destroyProduct: function () {
      axios.delete("/products/" + this.$route.params.id).then((response) => {
        console.log("Product successfully deleted", response.data);
        this.$router.push("/products");
      });
    },
  },
};
</script>

<template>
  <div class="products-show">
    <h1>{{ product.name }}</h1>
    <p>{{ product.description }}</p>
    <p>Price: {{ product.formatted.price }}</p>
    <p>Tax: {{ product.formatted.tax }}</p>
    <p>Total: {{ product.formatted.total }}</p>
    <router-link to="/products">Back to all products</router-link>
    |
    <router-link v-bind:to="`/products/${product.id}/edit`">Edit product</router-link>
    |
    <button v-on:click="destroyProduct()">Delete product</button>
  </div>
</template>
