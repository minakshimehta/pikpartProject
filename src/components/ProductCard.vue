<template>
    <div class="product-card">
      <!-- Product Image -->
      <img
        :src="product.images && product.images.length > 0 ? product.images[0] : defaultImage"
        :alt="product.title"
        class="product-image"
      />
  
      <!-- Product Title -->
      <h3>{{ product.title }}</h3>
  
      <!-- Price and Discount -->
      <p class="price"><strong>Price:</strong> ${{ product.price }}</p>
      <p class="discount"><strong>Discount:</strong> {{ product.discountPercentage }}%</p>
  
      <!-- Quantity Controls -->
      <div class="quantity-controls">
        <button @click="decreaseQuantity" class="quantity-btn decrease-btn">-</button>
        <input type="number" v-model="quantity" min="1" class="quantity-input" />
        <button @click="increaseQuantity" class="quantity-btn increase-btn">+</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      product: Object,
      onDelete: Function,
    },
    data() {
      return {
        quantity: 1,
        defaultImage: "https://via.placeholder.com/150", // Fallback image
      };
    },
    methods: {
      increaseQuantity() {
        this.quantity++;
      },
      decreaseQuantity() {
        if (this.quantity > 1) {
          this.quantity--;
        }
      },
      addToCart() {
        console.log("Adding product to cart...");
      },
      deleteProduct() {
        this.onDelete(this.product.id);
      },
    },
  };
  </script>
  
  <style scoped>
  .product-card {
    border-radius: 15px;
    padding: 20px;
    margin: 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    background: linear-gradient(135deg, #f0f0f0, #ffffff);
    width: 270px;
    height: auto;
    box-sizing: border-box;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .product-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  }
  
  .product-image {
    max-width: 100%;
    height: 180px;
    margin-bottom: 15px;
    border-radius: 8px;
    object-fit: cover;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }
  
  h3 {
    font-size: 1.2rem;
    color: #333;
    font-weight: 600;
    margin-bottom: 12px;
  }
  
  .price {
    font-size: 1rem;
    font-weight: 500;
    color: #444;
  }
  
  .discount {
    font-size: 0.9rem;
    color: #ff6f61; /* Discount color */
  }
  
  .quantity-controls {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 15px;
    margin: 20px 0;
  }
  
  .quantity-btn {
    font-size: 1.5rem;
    padding: 12px;
    width: 45px;
    height: 45px;
    border-radius: 50%;
    background-color: #007bff;
    color: white;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
    box-shadow: 0 4px 8px rgba(0, 123, 255, 0.3);
  }
  
  .quantity-btn:hover {
    background-color: #0056b3;
    transform: scale(1.1);
  }
  
  .quantity-btn:active {
    transform: scale(0.95);
  }
  
  .decrease-btn {
    background-color: #dc3545; /* Red for decrease */
  }
  
  .increase-btn {
    background-color: #28a745; /* Green for increase */
  }
  
  .quantity-input {
    width: 70px;
    padding: 10px;
    text-align: center;
    font-size: 1.2rem;
    border: 2px solid #ccc;
    border-radius: 15px;
    outline: none;
    transition: border-color 0.3s ease;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .quantity-input:focus {
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
  }
  
  @media (max-width: 768px) {
    .product-card {
      width: 230px;
    }
  }
  
  @media (max-width: 480px) {
    .product-card {
      width: 100%;
    }
  }
  </style>
  