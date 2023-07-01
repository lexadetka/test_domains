<template>
<div class="w-25">
  <input class="form-control" placeholder="data" v-model="value">
  <button @click="testPost" class="btn btn-outline-success">test Post</button>
  <div v-if="data">
    {{this.data}}
  </div>
</div>
</template>

<script>
import axios from "axios";

export default {
  name: "Post",
  data(){
    return{
      data: null,
      value: ''
    }
  },
  methods: {
    testPost(){
      axios.post('http://localhost:8000/api/post', {data: this.value})
          .then(res=> {
            this.data = res.data.data
          })
    }
  }
}
</script>

<style scoped>

</style>