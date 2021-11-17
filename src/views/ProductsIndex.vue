<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="product in products">
        <p>ID: {{ product.id }}</p>
        <p>Name: {{ product.name }}</p>
        <p>Price: {{ product.price }}</p>
        <router-link v-bind:to="`/products/${product.id}`">Show More Info</router-link>
      </li>
    </ul>
  </div>
</template>

<style></style>

<script>
  import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "All Products!",
        products: []
      };
    },
    created: function () {
      this.indexFunction();
    },
    methods: {
      indexFunction: function() {
        console.log("in the index function");
        axios
          .get(`/products`)
          .then(response => {
            console.log(response.data);
            this.products = response.data
          })
      }
    },
  };
</script>