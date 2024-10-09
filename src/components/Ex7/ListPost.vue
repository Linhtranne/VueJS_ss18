<template>
    <div>
      <h2>List of Products</h2>
      <input type="text" v-model="searchQuery" placeholder="Tìm kiếm theo tên" />
      <button @click="searchProduct">Tìm kiếm</button>
      <div v-for="product in filteredProducts" :key="product.id">
        <img :src="product.image" :alt="product.name" width="100" />
        <h3>{{ product.name }}</h3>
        <p>{{ product.price }} VND</p>
        <button @click="viewDetails(product.id)">Xem chi tiết</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchQuery: '',
        products: [
          { id: 1, name: "Điện thoại iPhone 15 Pro", price: "30.000.000", image: "link-to-image-1" },
          { id: 2, name: "Điện thoại OPPO Reno11 5G", price: "10.500.000", image: "link-to-image-2" },
          { id: 3, name: "Điện thoại Vivo Y17s", price: "3.300.000", image: "link-to-image-3" }
        ]
      };
    },
    computed: {
      filteredProducts() {

        return this.products.filter(product => 
          product.name.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }
    },
    methods: {
      viewDetails(id) {

        this.$router.push(`/product-detail/${id}`);
      },
      searchProduct() {
        // Update URL with search query
        this.$router.push({ path: '/list-product', query: { name: this.searchQuery } });
      }
    },
    created() {
      // Save products to localStorage
      localStorage.setItem('products', JSON.stringify(this.products));
  
      // If query exists in the URL, perform search
      if (this.$route.query.name) {
        this.searchQuery = this.$route.query.name;
      }
    }
  };
  </script>
  