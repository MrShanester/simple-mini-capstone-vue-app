<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>Product Name:</p>
    <input type="string" v-model="newProductParams.name" />
    <p>Product Description:</p>
    <input type="text" v-model="newProductParams.description" />
    <p>Product Price:</p>
    <input type="integer" v-model="newProductParams.price" />
    <p>Product Image URL:</p>
    <input type="string" v-model="newProductParams.image_url" />
    <p></p>
    <button v-on:click="createProduct()">Create Product!</button>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <img v-bind:src="product.image_url" v-bind:alt="product.title" />
      <p>Price: ${{ product.price }}</p>
      <p>------------------------------------</p>
    </div>
    <button v-on:click="showHidden()">Click to See a Hidden Message!</button>
    <p>{{ hidden }}</p>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  border: 12px solid;
  border-image: linear-gradient(135deg, #ff0000 0%, #49ff33 25%, #3364ff 50%, #f6ff33 75%, #ff00a8 100%) 1;
}

img {
  width: 350px;
}
</style>

<script>
const axios = require("axios");

export default {
  data: function () {
    return {
      message: "Welcome To The Shop",
      products: [],
      hidden: "",
      newProductParams: {},
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products").then((response) => {
        this.products = response.data;
      });
    },
    showHidden: function () {
      this.hidden = "You're the Best!";
      this.setTimeout();
    },
    createProduct: function () {
      axios.post("http://localhost:3000/products", this.newProductParams).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
      this.newProductParams.name = "";
      this.newProductParams.description = "";
      this.newProductParams.price = "";
      this.newProductParams.image_url = "";
    },
  },
};
</script>
