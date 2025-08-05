<template>
   <div>API Calls</div>
   <div v-for="user in userObj.users">
      <h2>{{ user.name }}</h2>
      <p>{{ user.email }}</p>
      <hr />
   </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";
import axios from "axios";

const userObj = reactive({
   users: [],
});

onMounted(() => {
   axios
      .get("https://jsonplaceholder.typicode.com/todos/1/users")
      .then((response) => {
         console.log(response.data);
         userObj.users = response.data;
      });
});
</script>
