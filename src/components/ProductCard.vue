<template>
  <div class="product-card">
    <img :src="product.image" alt="Product Image">
    <router-link :to="`/product/${product.id}`">
      <h2>{{ product.name }}</h2>
    </router-link>
      <p>{{ product.description }}</p>
      <div class="product-details">
        <div class="product-price">
          <p class="price">$ {{ product.price }}</p>
        </div>
        <div class="product-controls">
          <input type="number" v-model="quantity" min="1" class="quantity-input" />
          <button @click="addToCart">Add to Cart</button>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: ['product'],
  data() {
    return {
      quantity: 1
    }
  },
  methods: {
    incrementQuantity() {
      this.quantity++
    },
    decrementQuantity() {
      if (this.quantity > 1) {
        this.quantity--
      }
    },
    addToCart() {
      // Add the product and quantity to the cart
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<style scoped>
.product-card {
  width: 260px;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 12px;
  background-color: #fff;
  text-align: center;
}

.product-card img {
  width: 100%;
  height: 180px;
  object-fit: contain;
}

.product-card h2 {
  font-size: 18px;
  margin: 10px 0;
}

.product-card p {
  font-size: 14px;
}

.product-details {
  margin-top: 10px;
}

.product-controls {
  margin-top: 10px;
}
</style>