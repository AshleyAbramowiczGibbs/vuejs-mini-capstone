<template>
  <div class="home">
   <!--  <img src="../assets/Dresses.jpg" alt=""> -->
    <div class="circular" v-bind:style="{ 'background-image': '../assets/Dresses.jpg' }"></div>

    <div class="container">
      <div class="jumbotron">
        <h1 class="display-4">Bridesmaid Dress Resale</h1>
        <p class="lead">
          This is a simple hero unit, a simple jumbotron-style component for
          calling extra attention to featured content or information.
        </p>
        <hr class="my-4" />
        <p>
          It uses utility classes for typography and spacing to space content
          out within the larger container.
        </p>
        <a class="btn btn-primary btn-lg" href="#" role="button"
          >Buy a dress!</a
        >
        <br />
        <a class="btn btn-primary btn-lg" href="#" role="button"
          >Sell a dress!</a
        >
      </div>
      <div class="row">
        <div v-for="product in products" class="col-md-4 mb-2">
          <div class="card">
            <img
              class="card-img-top"
              v-bind:src="getImageFromProduct(product)"
              alt="Card image cap"
            />
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">Chef: {{ product.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
body {
  font-family: Candara, Calibri, Segoe, "Segoe UI", Optima, Arial, sans-serif;
}

.jumbotron {
  opacity: 0.8;
}

.btn-primary {
  background: #b76e79;
  border: white;
}
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
    axios.get("http://localhost:3000/api/products").then(
      function(response) {
        console.log(response.data);
        this.products = response.data;
      }.bind(this)
    );
  },
  methods: {
    getImageFromProduct: function(product) {
      if (product.image[0]) {
        return product.image[0].url;
      } else {
        return "https://cdn7.bigcommerce.com/s-yd0nd8/images/stencil/1280x1280/products/169/5820/Revelry_074__56124.1540512985.jpg?c=2&imbypass=on";
      }
    }
  },
  computed: {}
};
</script>
