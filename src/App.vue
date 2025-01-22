<template>
  <div id="app">
    <h1>Product List</h1>
    <div class="product-container">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProductCard from "./components/ProductCard.vue";

export default {
  name: "App",
  components: {
    ProductCard
  },
  data() {
    return {
      products: []
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      axios
        .get("https://dummyjson.com/products")
        .then((response) => {
          this.products = response.data.products;
        })
        .catch((error) => {
          console.error("Error fetching products:", error);
        });
    },
    
  }
};
</script>

<style>
#app {
  font-family: 'Poppins', sans-serif;
  padding: 20px;
  text-align: center;
  background-color: #f4f7f6; 
  color: #333; 
}

h1, h2, h3 {
  font-weight: 600;
  margin-bottom: 20px;
}

p {
  font-weight: 400;
  line-height: 1.6;
  font-size: 1.1rem;
}


.product-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  margin-top: 20px;
}
</style>