<template>
  <div class="edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="editProductParams.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model="editProductParams.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="editProductParams.description" />
      </div>
      <div>
        <label>Supplier ID:</label>
        <input type="text" v-model="editProductParams.supplier_id" />
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
        editProductParams: {},
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
            this.editProductParams = response.data;
          })
      }
    },
  };
</script>