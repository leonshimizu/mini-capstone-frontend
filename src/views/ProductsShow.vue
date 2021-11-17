<template>
  <div class="show-edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="Product.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model="Product.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="Product.description" />
      </div>
      <div>
        <label>Supplier ID:</label>
        <input type="text" v-model="Product.supplier_id" />
      </div>
      <input type="submit" value="Update" />
      <br>
    </form>
    <button v-on:click="deleteFunction()">Delete</button>
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
  export default {
    data: function () {
      return {
        Product: {},
        errors: []
      };
    },
    created: function () {
      this.showFunction();
    },
    methods: {
      submit: function () {
        console.log("in the edit Function")
        axios
          .patch(`/products/${this.$route.params.id}`, this.editProductParams)
          .then(response => {
            console.log(response.data);
            this.$router.push('/products');
          })
      },
      showFunction: function() {
        console.log("in the show function");
        axios
          .get(`/products/${this.$route.params.id}`)
          .then(response => {
            console.log(response.data);
            this.Product = response.data;
          })
      },
      deleteFunction() {
        console.log("in the delete function");
        axios
          .delete(`/products/${this.$route.params.id}`)
          .then(response => {
            console.log(response.data);
            this.$router.push('/products');
          })
      }
    },
  };
</script>