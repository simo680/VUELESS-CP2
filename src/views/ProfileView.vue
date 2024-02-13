<template>
  <div>
    <div class="info">
      <div class="info__profile">
        <span>Username: {{ this.response.username}}</span>
        <span>Name: {{ this.response.firstname}}</span>
        <span>LastName: {{ this.response.lastName}}</span>
        <span>Gender: {{this.response.gender}}</span>
        <span>Email: {{ this.response.email}}</span>
      </div>
      <img :src="this.response.image" alt="" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
       response: {},
       error: "",
    }
  },
  mounted() {
    axios
      .get('https://dummyjson.com/auth/me', {
        headers: {
          Authorization: `Bearer ${localStorage.getItem('token')}`
        }
      })
      .then((response) => {
        const data = response.data
        if (data.message) {
          this.error = data.message
        } else {
          this.response = data
        }
      })
      .catch((error) => {

        console.error(error)
        this.res.message = error.response.data.message;
      })
  }
}
</script>

<style></style>
