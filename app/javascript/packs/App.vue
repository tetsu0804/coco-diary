<template>
  <div id="app">
    <b-container>
      <Header></Header>
      <p>{{ message }}</p>
      <router-view></router-view>
    </b-container>
  </div>
</template>

<script>
import axios from 'axios'
import Header from '../components/Header.vue'

export default {
  data: function () {
    return {
      message: "Hello Vue!",
      //first_name: '',
      //users: []
    }
  },
  components: {
    Header: Header
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
