<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="product in products">
        <p>Name: {{ product.name }}</p>
        <p>Price: {{ product.price }}</p>
        <button v-on:click="showModal(product)">Show More Info</button>
      </li>
    </ul>
    <dialog id="show-modal">
      <form method="dialog">
        <p>ID: {{ currentProduct.id }}</p>
        <p>Name: {{ currentProduct.name }}</p>
        <p>Price: {{ currentProduct.price }}</p>
        <p>Tax: {{ currentProduct.tax }}</p>
        <p>Total: {{ currentProduct.total }}</p>
        <p>Description: {{ currentProduct.description }}</p>
        <p>Supplier ID: {{ currentProduct.supplier_id }}</p>
        <router-link v-bind:to="`/products/${currentProduct.id}`">Edit Product</router-link>
        <br>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
  import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "All Products!",
        products: [],
        currentProduct: {}
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
      },
      showModal: function(theProduct) {
        console.log("in the show modal");
        document.querySelector("#show-modal").showModal();
        this.currentProduct = theProduct;
      }
    },
  };
</script>