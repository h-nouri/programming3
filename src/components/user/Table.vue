<script setup>
import { defineProps } from 'vue';
import 'bootstrap-icons/font/bootstrap-icons.css'
const props = defineProps({
   users:Object
})
</script>
<template>
  <table class="table table-striped mt-4">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Name</th>
        <th scope="col">Username</th>
        <th scope="col">Phone</th>
        <th scope="col">Email</th>
        <th scope="col">Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(user,index) in users" :key="user.id">
        <td scope="row">{{index + 1}}</td>
        <td v-text="user.name"></td>
        <td v-text="user.username"></td>
        <td v-text="user.phone"></td>
        <td v-text="user.email"></td>
        <td>
            <a href="#" class="p-2">
                <i class="bi bi-eye-fill"></i>
            </a>
            <a href="#" class="text-success p-2">
                <i class="bi bi-pencil-fill"></i>
            </a>
            <a href="#" class="text-danger p-2">
                <i class="bi bi-trash-fill"></i>
            </a>
        </td>
      </tr>
      
    </tbody>
  </table>
</template>
<style scoped>
thead th{
    background-color: black;
    color: white;
}
</style>