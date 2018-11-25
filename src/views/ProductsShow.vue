<template>
  <div class="home">
    <h1>This is a dress!!!</h1>
    {{ product }}

    <a href="/#/">Back to all products</a>
  </div>
</template>

<style>
</style>

<script>
  var axios = require("axios");
export default {
    data: function() {
      return {
        product: {}
      };
    },
    created: function() {
      axios.get("http://localhost:3000/api/products/" + this.$route.params.id).then(response => {
        console.log(response.data);
        this.product = response.data;
      });
    },
    methods: {},
    computed: {}
};
</script>