<template>
  <div class="home">
    <!-- <img src="../assets/Dresses.jpg" alt=""> -->
    <div
      class="circular"
      v-bind:style="{ 'background-image': '../assets/Dresses.jpg' }"
    ></div>

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
        <br>

        name: <input v-model="newProductName" type="text">
        description: <input v-model="newProductDescription" type="text">
        alteration_information: <input v-model="newProductAlterationInfo" type="text">
        size: <input v-model="newProductSize" type="text">
        color_one: <input v-model="newProductColorOne" type="text">
        color_two: <input v-model="newProductColorTwo" type="text">
        brand: <input v-model="newProductBrand" type="text">
        length:<input v-model="newProductLength" type="text"> 
        condition: <input v-model="newProductCondition" type="text">
        original_price: <input v-model="newProductOriginalPrice" type="text">
        selling_price: <input v-model="newProductSellingPrice" type="text">
        <button v-on:click="addDress();" class="btn btn-primary btn-lg">
          Sell a dress!
        </button>

      </div>
      <h1>Search for A Dress</h1>
      <input type="text" v-model="searchFilter" list="names">
      <datalist id="names">
        <option v-for="product in products">{{ product.name }}</option>
      </datalist>
      <div class="row">
        <div v-for="product in filterBy(products, searchFilter, 'name', 'description')" class="col-md-4 mb-2">
          <div class="card">
            <img
              class="card-img-top"
              v-bind:src="getImageFromProduct(product)"
              alt="Card image cap"
            />
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">Description: {{ product.description }}</p>

            </div>
              <a v-bind:href="'/#/products/' + product.id" class="btn btn-primary">Show Information</a>
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
      products: [],
      newProductName: "",
      newProductDescription: "",
      newProductAlterationInfo: "",
      newProductSize: "",
      newProductColorOne: "",
      newProductColorTwo: "",
      newProductBrand: "",
      newProductLength: "",
      newProductCondition: "",
      newProductOriginalPrice: "",
      newProductSellingPrice: "",
      searchFilter: ""
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
    },
    addDress: function() {
      console.log("add a dress!!!!");
      let params = {
        Name: this.newProductName,
        Descirption: this.newProductDescription,
        alteration_information: this.newProductAlterationInfo,
        size: this.newProductSize,
        color_one: this.newProductColorOne,
        color_two: this.newProductColorTwo,
        brand: this.newProductBrand,
        length: this.newProductLength,
        condition: this.newProductCondition,
        original_price: this.newProductOriginalPrice,
        selling_price: this.newProductSellingPrice
      };
      axios.post("http://localhost:3000/api/products", params).then(
        function(response) {
          console.log(response);
          this.products.push(response.data);
        }.bind(this)
      ).catch(function(error) {
        console.log(error.response);
      });
    }
  },
  computed: {}
};
</script>
