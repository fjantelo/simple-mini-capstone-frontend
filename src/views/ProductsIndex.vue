<script>
import axios from "axios";
import moment from "moment";

export default {
  data: function () {
    return {
      products: [],
      currentProduct: {},
      nameFilter: "",
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
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
    filterProducts: function () {
      return this.products.filter((product) => {
        var lowerNameFilter = this.nameFilter.toLowerCase();
        var lowerName = product.name.toLowerCase();
        return lowerName.includes(lowerNameFilter);
      });
    },
  },
};
</script>

<template>
  <div>
    Search:
    <input type="text" v-model="nameFilter" list="names" />
    <datalist id="names">
      <option v-for="product in products" v-bind:key="product.id">{{ product.name }}</option>
    </datalist>
  </div>
  <TransitionGroup name="list">
    <div
      v-for="product in filterProducts()"
      v-bind:key="product.id"
      v-on:click="currentProduct = product"
      v-bind:class="{ selected: product === currentProduct }"
    >
      <h3>
        <router-link :to="`/products/${product.id}`">{{ product.name }}</router-link>
      </h3>
      <p>{{ product.formatted.price }}</p>
      <p>Created: {{ relativeDate(product.created_at) }}</p>
      <img v-bind:src="product.image_url" :alt="product.name" />
    </div>
  </TransitionGroup>
</template>

<style>
.selected {
  color: dodgerblue;
  background-color: chartreuse;
}
.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
  transition: all 0.7s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
  position: absolute;
}
</style>
