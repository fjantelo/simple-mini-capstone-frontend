<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editProductParams: {},
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id + ".json").then((response) => {
      this.editProductParams = response.data;
    });
  },
  methods: {
    editProduct: function () {
      axios
        .patch("http://localhost:3000/products/" + this.editProductParams.id + ".json", this.editProductParams)
        .then((response) => {
          console.log("Successfully updated product!", response.data);
          this.$router.push("/products");
        })
        .catch((error) => {
          this.errors = error.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="products-show">
    <p>
      Name:
      <input type="text" v-model="editProductParams.name" />
    </p>
    <p>
      Price:
      <input type="text" v-model="editProductParams.price" />
    </p>
    <p>
      Description:
      <input type="text" v-model="editProductParams.description" />
    </p>
    <p>
      Image URL:
      <input type="text" v-model="editProductParams.image_url" />
    </p>
    <button v-on:click="editProduct()">Edit product</button>
    <!-- <input type="submit" value="Submit" /> -->
    <p></p>
    <router-link to="/products">Back to all products</router-link>
  </div>
</template>
