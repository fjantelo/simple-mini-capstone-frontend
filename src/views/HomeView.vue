<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      newProductParams: {},
      currentProduct: {},
      formattedPrice: {},
      editProductParams: {},
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
    createProduct: function () {
      axios.post("http://localhost:3000/products.json", this.newProductParams).then((response) => {
        console.log("Product created", response.data).catch((error) => console.log(error.response));
        this.products.push(response.data);
      });
      this.newProductParams = {};
    },
    showProduct: function (product) {
      console.log(product);
      this.currentProduct = product;
      this.editProductParams = product;
      this.formattedPrice = product.formatted;
      document.querySelector("#product-details").showModal();
    },
    updateProduct: function (product) {
      axios.patch("http://localhost:3000/products/" + product.id, this.editProductParams).then((response) => {
        console.log("Successfully updated product!", response.data);
      });
    },
    destroyProduct: function (product) {
      axios.delete("http://localhost:3000/products/" + product.id).then((response) => {
        console.log("Successfully deleted product!", response.data);
        var index = this.products.indexOf(product);
        this.products.splice(index, 1);
      });
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
      <button v-on:click="showProduct(product)">More Information</button>
    </div>
    <dialog id="product-details">
      <form method="dialog">
        <h2>Product Info</h2>
        <p>
          Name:
          <input type="text" v-model="editProductParams.name" />
        </p>
        <p>
          Price:
          <input type="text" v-model="editProductParams.price" />
        </p>
        <p>Tax: {{ formattedPrice.tax }}</p>
        <p>Total: {{ formattedPrice.total }}</p>
        <p>
          Description:
          <input type="text" v-model="editProductParams.description" />
        </p>
        <p>
          Image URL:
          <input type="text" v-model="editProductParams.image_url" />
        </p>
        <button v-on:click="updateProduct(currentProduct)">Update Product</button>
        <button v-on:click="destroyProduct(currentProduct)">Delete Product</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
.bluetext {
  color: blue;
}
</style>
