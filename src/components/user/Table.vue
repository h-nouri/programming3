<script setup>
import { defineProps } from 'vue';
import 'bootstrap-icons/font/bootstrap-icons.css'
import Swal from 'sweetalert2';
import axios from 'axios';
const props = defineProps({
  users: Object
})
function showDeleteConfirmation(id) {
  Swal.fire({
    title: "Do you want to remove the user?",
    showCancelButton: true,
    confirmButtonText: "Delete",
  }).then((result) => {
    /* Read more about isConfirmed, isDenied below */
    if (result.isConfirmed) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/users/${id}`)
        .then(function (response) {
          // handle success
          Swal.fire("Deleted!", "", "success");

        })
        .catch(function (error) {
          // handle error
          console.log(error);
        })
        .finally(function () {
          // always executed
        });


    }
  });
}
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
      <tr v-for="(user, index) in users" :key="user.id">
        <td scope="row">{{ index + 1 }}</td>
        <td v-text="user.name"></td>
        <td v-text="user.username"></td>
        <td v-text="user.phone"></td>
        <td v-text="user.email"></td>
        <td>
          <router-link :to="{ name: 'showUser', params: { id: user.id } }" class="p-2">
            <i class="bi bi-eye-fill"></i>
          </router-link>
          <router-link :to="{ name: 'editUser', params: { id: user.id } }" class="text-success p-2">
            <i class="bi bi-pencil-fill"></i>
          </router-link>

          <a @click.prevent="showDeleteConfirmation(user.id)" href="#" class="text-danger p-2">
            <i class="bi bi-trash-fill"></i>
          </a>
        </td>
      </tr>

    </tbody>
  </table>
</template>
<style scoped>
thead th {
  background-color: black;
  color: white;
}
</style>