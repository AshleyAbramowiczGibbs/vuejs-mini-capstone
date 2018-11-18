<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in products">
      <h2>{{ product.name }}</h2>
      <p>{{ product.description }}</p>
    </div>
  </div>
</template>

<style>
</style>

<script>
  let axios = require("axios");
export default {
    data: function() {
      return {
        message: "Welcome to Vue.js!",
        products: []
      };
    },
    created: function() {
      axios.get("http://localhost:3000/api/products").then(function(response) {
        console.log(response.data);
        this.products = response.data;
      }.bind(this)
      );
    },
    methods: {},
    computed: {}
};
</script>