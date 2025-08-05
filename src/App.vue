<template>
   <div>API Calls</div>
   <hr />
   <div v-for="user in userObj.users">
      <h3>{{ user.name }}</h3>
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
   fetch("https://jsonplaceholder.typicode.com/todos/1/users")
      .then((response) => response.json())
      .then((data) => {
         console.log(data);
         userObj.users = data;
      });

   /*axios
      .get("https://jsonplaceholder.typicode.com/todos/1/users")
      .then((response) => {
         console.log(response.data);
         userObj.users = response.data;
      });
   */
});
</script>
