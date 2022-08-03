<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newProductParams: { name: "", description: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createProduct: function () {
      axios
        .post("/products.json", this.newProductParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/products");
          localStorage.setItem("flashMessage", "Product created!");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>

<template>
  <div class="products-new">
    <form v-on:submit.prevent="createProduct()">
      <h1>New Product</h1>
      <img v-if="status" :src="`https://http.dog/${status}.jpg`" alt="" />
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newProductParams.name" />
        <small v-if="newProductParams.name.length <= 30">
          Characters remaining: {{ 30 - newProductParams.name.length }}
        </small>
        <small v-if="newProductParams.name.length > 30" class="text-danger">
          Name must be less than 30 characters!
        </small>
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="newProductParams.description" />
        <small
          v-if="newProductParams.description.length > 0 && newProductParams.description.length < 6"
          class="text-danger"
        >
          Must be at least 6 characters
        </small>
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
