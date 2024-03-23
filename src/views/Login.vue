<template>
  <form @submit.prevent="login">
    <div>
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="username" required>
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="password" required>
    </div>
    <div>
      <button type="submit">Login</button>
    </div>
  </form>
</template>


<script>
import Home from '../views/Home.vue';
export default {
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    login() {
      
      if (this.username === 'admin' && this.password === 'admin') {
        alert("Login successfully");
        this.$router.push('/');       
      } else {
        // Authentication failed
        alert('Invalid username or password');
      }
    }
  }
};
</script>

<style>

form {
  max-width: 300px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

</style>