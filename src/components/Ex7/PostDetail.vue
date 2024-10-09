<template>
    <div v-if="product">
      <h2>Chi tiết sản phẩm</h2>
      <img :src="product.image" :alt="product.name" width="200" />
      <p><strong>Id:</strong> {{ product.id }}</p>
      <p><strong>Product Name:</strong> {{ product.name }}</p>
      <p><strong>Price:</strong> {{ product.price }} VND</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        product: null
      };
    },
    created() {
      const id = this.$route.params.id;
      const products = JSON.parse(localStorage.getItem('products'));
      this.product = products.find(product => product.id === parseInt(id));
    }
  };
  </script>
  