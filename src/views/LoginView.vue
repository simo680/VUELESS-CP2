<template>

  <form @submit.prevent="handleSubmit" class="">
    <h2>Authorization</h2>
    <p style="color: red" v-if="res.message">{{res.message }}</p>
    <label>Login</label>
    <input type="text" class="" v-model="username" placeholder="username" />
    <label>Password</label>
    <input type="password" class="" v-model="password" placeholder="Password" autocomplete="on" />
    <button>Submit</button>
  </form>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      username: '',
      password: '',
      res: {},
    }
  },
  methods: {
       async handleSubmit() {
  try {
    const response = await axios.post('https://dummyjson.com/auth/login', {
      username: this.username, 
      password: this.password,
    });
    console.log(response); 
    this.res = response.data;

    if (this.res.token) {
      localStorage.setItem('token', this.res.token);
    } else {
      localStorage.removeItem('token');
    }
  } catch (error) {
    console.error(error);
  }
}
  }
}
</script>

<style scoped></style>
