<template>
  <div class="newProduct">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>Sell a dress!</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Name:</label> 
          <input type="text" class="form-control" v-model="name">
        </div>
        <div class="form-group">
          <label>Description:</label>
          <input type="text" class="form-control" v-model="description">
        </div>
        <div class="form-group">
          <label>Size:</label> 
          <input type="text" class="form-control" v-model="size">
        </div>
        <div class="form-group">
          <label>Condition:</label>
          <input type="text" class="form-control" v-model="Condition">
        </div>
        <input type="submit" class="btn btn-primary" value="Submit">
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      name: "",
      description: "",
      size: "",
      condition: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        name: this.name,
        email: this.description,
        size: this.size,
        condition: this.condition
      };
      axios
        .post("http://localhost:3000/api/products", params)
        .then(response => {
          this.$router.push("/newProduct");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>