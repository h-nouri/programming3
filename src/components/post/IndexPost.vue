<script setup>
import axios from 'axios';
import { onMounted,ref } from 'vue';
import Table from './Table.vue'
let all_posts=ref(null)
function get_posts(){
    axios
    .get("https://jsonplaceholder.typicode.com/posts")
    .then(function (response) {
      // handle success
      all_posts.value = response.data;
      console.log(response.data);
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .finally(function () {
      // always executed
    });
}
onMounted(()=>{
    get_posts()
})
</script>
<template>
    <Table :posts="all_posts"/>
</template>