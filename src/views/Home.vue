<template>

  <div>
    <h1>Shopping Cart</h1>
    <div>
      <h2>Products</h2>
      <div class="products-container">
        <div v-for="product in products" :key="product.id" class="product-box">
          <p>{{ product.name }} - ₱{{ product.price }}</p>
          <button @click="addToCart(product)">Add to Cart</button>
        </div>
      </div>
    </div>
  
    <div class="cart-container">
      <h2>Cart</h2>
      <ul>
        <li v-for="item in cart" :key="item.product.id">
          {{ item.product.name }} - ₱{{ item.product.price }} - Qty: {{ item.quantity }}
          <button @click="removeFromCart(item)">Remove</button>
          <input type="number" min="1" v-model="item.quantity" @change="updateQuantity(item)">
        </li>
      </ul>
      <p style="text-align: center;">Total: ₱{{ total }}</p>
    </div>
  </div>
</template>



  <script>
    export default {
      name: 'App',
      data() {
        return {
        products: [
          { id: 1, name: 'Apple',  price: 25},
          { id: 2, name: 'Orange',  price: 20 },
          { id: 3, name: 'Banana', price: 35 },
         { id: 4, name: 'Grapes',  price: 200 }
        ],
          cart: [],
          isAuthenticated: true
    };
  },
  computed: {
    total() {
      return this.cart.reduce((total, item) => {
        return total + (item.product.price * item.quantity);
      }, 0);
    }
  },

  methods: {
    addToCart(product) {
      if (!this.isAuthenticated) {
      // Redirect to login page if user is not authenticated
         this.$router.push('/login');
      } else {
    // Add product to cart
    const existingItem = this.cart.find(item => item.product.id === product.id);
    if (existingItem) {
      existingItem.quantity++;
    } else {
      this.cart.push({ product: product, quantity: 1 });
     }
   }
  },
    
    removeFromCart(item) {
      const index = this.cart.indexOf(item);
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
    },
    updateQuantity(item) {
      item.quantity = parseInt(item.quantity) || 1;
    },
    onLoginSuccess() {
      // Update authentication status upon successful login
      this.isAuthenticated = true;
      // Redirect back to home after login
      this.$router.push('/');
    }
  }
};
</script>

<style>


    h1{
        text-align: center;
    }

    h2{
        text-align: center;
    }
   
    button {
      background-color:  limegreen;
      color: white;
      padding: 5px 10px;
      border: 2px solid black;
      cursor: pointer;
      margin-bottom: 10px;
      width: auto;
    }

    button:hover {
      background-color: darkgreen;
    }

   .products-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
   
    
  }

  .product-box {
    border: 2px solid black;
    padding: 10px;
    margin-bottom: 10px;
    width: 200px;
    text-align: center;
    background-color: yellow;

  }

  .product-box button {
    margin-top: 10px;
  }

  .cart-container {
    border: 2px solid black;
    padding: 10px;
    margin-top: 20px;
    background-color: yellow;
    width: 480px;
    height: 250px;
    text-align: center;
    margin-left: auto;
    margin-right: auto;
}

  .cart-container h2 {
    margin-top: 0;
  }

</style>