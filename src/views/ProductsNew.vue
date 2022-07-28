<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newProductParams: {},
      errors: [],
    };
  },
  methods: {
    createProduct: function () {
      axios
        .post("/products.json", this.newProductParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/products");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="products-new">
    <form v-on:submit.prevent="createProduct()">
      <h1>New Product</h1>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newProductParams.name" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="newProductParams.description" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model="newProductParams.price" />
      </div>
      <div>
        <label>Image URL:</label>
        <input type="text" v-model="newProductParams.image_url" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
