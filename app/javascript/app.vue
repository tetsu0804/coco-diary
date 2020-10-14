<template>
  <div id="app">
    <p>{{ message }}</p>
    <form v-on:submit="onSubmit">
      タイトル
      <input v-model="first_name">
      <button type="submit">登録</button>
    </form>
    <div v-for="user in users" :key="user.id">
      <p>{{ user.first_name }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data: function () {
    return {
      message: "Hello Vue!",
      first_name: '',
      users: []
    }
  },
  mounted() {
    axios.get('/api/v1/users')
    .then(response => {
      this.users = response.data.users
    })
  },
  methods: {
    onSubmit() {
      axios.post('/api/v1/user', {first_name: this.first_name})
      .then(response => {
        this.first_name = ''
      })
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
