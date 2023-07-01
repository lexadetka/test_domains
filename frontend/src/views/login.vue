<script setup>
import { RouterLink, RouterView } from 'vue-router'
import 'bootstrap/dist/css/bootstrap.css'
axios.defaults.withCredentials=true
</script>

<template>
  <div class="w-25">
    <input type="text" class="form-control" v-model="email" placeholder="email">
    <input type="password" class="form-control" v-model="password" placeholder="password">
    <button class="btn btn-success" @click="login">Login</button>
  </div>
  <button class="btn btn-primary" @click="getUser">Get user</button>
  <div v-if="data">
    {{this.data}}
  </div>
  <div>
    <button class="btn btn-success" @click.prevent="$router.push({name: 'post'})">test post page</button>
  </div>

</template>
<script>
import 'bootstrap/dist/js/bootstrap'
import axios from 'axios'
export default {
  name: 'App',
  data(){
    return{
      email: '',
      password: '',
      data: null
    }
  },
  methods: {
    login(){
      axios.get('http://localhost:8000/sanctum/csrf-cookie')
          .then(res=>{
            axios.post('http://localhost:8000/login', {email: this.email, password: this.password})
                .then(res=>{
                  console.log(res)
                })
          })
    },
    getUser(){
      axios.get('http://localhost:8000/api/user')
          .then(res=>{
            this.data = res.data
          })
    }
  }
}
</script>
<style scoped>

</style>
