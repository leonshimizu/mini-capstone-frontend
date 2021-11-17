<template>
  <div class="create">
    <form v-on:submit.prevent="submit()">
      <h1>Add Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newProductParams.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model="newProductParams.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="newProductParams.description" />
      </div>
      <div>
        <label>Supplier ID:</label>
        <input type="text" v-model="newProductParams.supplier_id" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
  export default {
    data: function () {
      return {
        newProductParams: {},
        errors: []
      };
    },
    created: function () {},
    methods: {
      submit: function () {
        console.log("in the create Function")
        axios
          .post('/products', this.newProductParams)
          .then(response => {
            console.log(response.data);
            this.$router.push('/products');
          })
      }
    },
  };
</script>