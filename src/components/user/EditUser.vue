<script setup>
import { onMounted, ref, watch,reactive } from "vue";
import { useRoute,useRouter } from "vue-router";
import axios from "axios";
import Swal from "sweetalert2";
let user = ref(null)
const router=useRouter()
const route = useRoute();
let userId=route.params.id
let usernameError = ref('')
let emailError = ref('')
let loading = ref(false)

let form = reactive({
  name: '',
  phone: '',
  email: '',
  username: ''
})
function get_user(id) {
  axios
    .get(`https://jsonplaceholder.typicode.com/users/${id}`)
    .then(function (response) {
      // handle success
      user.value = response.data;
      form.name=response.data.name
      form.phone=response.data.phone
      form.username=response.data.username
      form.email=response.data.email
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .finally(function () {
      // always executed
    });
}
function validator() {
  if (form.username == '')
    usernameError.value = "Username is required!"
  else
    usernameError.value = ""

  if (form.email == '')
    emailError.value = "email is required!"
  else
    emailError.value = ""

  if (form.username !== "" && form.email !== "") {
    UpdateUser(userId)
  }

}
onMounted(() => {
  get_user(route.params.id);
});
watch(() => route.params.id, (new_id) => {
  get_user(new_id)
})

function UpdateUser(id){
  loading.value=true
  axios
    .put(`https://jsonplaceholder.typicode.com/users/${id}`, {
      name: form.name,
      username: form.username,
      email: form.email,
      phone: form.phone,
    })
    .then(function (response) {
      // handle success
      loading.value=false
      Swal.fire({
        title: "User Updated!",
        icon: "success",
        draggable: true
      });
      router.push({name:'indexUser'})

    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .finally(function () {
      // always executed
    });
}
</script>
<template>
  <div class="container">
    <h1>edit</h1>
    <div class="row" v-if="user != null">
      <div class="col-12">
        <form>
          <div class="mb-3">
            <label for="exampleFormControlInput1" class="form-label">Name</label>
            <input v-model="form.name" type="text" class="form-control" id="exampleFormControlInput1"
              placeholder="Name">
          </div>
          <div class="mb-3">
            <label for="exampleFormControlInput2" class="form-label">phone</label>
            <input v-model="form.phone" type="text" class="form-control" id="exampleFormControlInput2"
              placeholder="Phone">
          </div>
          <div class="mb-3">
            <label for="exampleFormControlInput3" class="form-label">Username</label>
            <input v-model="form.username" type="text" class="form-control" id="exampleFormControlInput3"
              placeholder="username">
            <span class="text-danger">{{ usernameError }}</span>
          </div>
          <div class="mb-3">
            <label for="exampleFormControlInput4" class="form-label">Email address</label>
            <input v-model="form.email" type="email" class="form-control" id="exampleFormControlInput4"
              placeholder="name@example.com">
            <span class="text-danger">{{ emailError }}</span>
          </div>
          <router-link :to="{ name: 'indexUser' }" class="btn btn-secondary">Cancel</router-link>
          <button @click.prevent="validator" class="btn btn-success ms-2">
            <span v-if="loading" class="spinner-border spinner-border-sm" aria-hidden="true"></span>
            <span>Update</span>
          </button>
        </form>
      </div>
    </div>
    <div v-else>
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
  </div>
</template>