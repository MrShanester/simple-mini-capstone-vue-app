<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p></p>
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
    },
  },
};
</script>
