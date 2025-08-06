<template>
   <div v-if="destinationObj.isLoading" class="d-flex justify-content-center p-4">
      <span class="loader"></span>
   </div>
   <div v-else class="container p-4 bg-white">
      <div>
         <h1 class="text-success text-center">Travel</h1>
      </div>
      <hr />
      <table class="table table-striped table-light">
         <thead>
            <tr>
               <th>Name</th>
               <th>Days</th>
               <th>Price</th>
            </tr>
         </thead>
         <tbody>
            <tr
               class="table-light"
               v-for="destination in destinationObj.destinationList"
               :key="destination.id"
            >
               <td>{{ destination.name }}</td>
               <td>{{ destination.days }}</td>
               <td>{{ destination.price }}</td>
            </tr>
         </tbody>
      </table>
   </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";
import axios from "axios";

const destinationObj = reactive({
   destinationList: [],
   isLoading: false,
});

onMounted(() => {
   loadDestination();
});

function loadDestination() {
   destinationObj.isLoading = true;
   axios.get("http://localhost:3000/destination").then((response) => {
      new Promise((resolve) => setTimeout(resolve, 1000)).then(() => {
         console.log(response.data);
         destinationObj.destinationList = response.data;
         destinationObj.isLoading = false;
      });
   });
}
</script>

<style scoped>
.loader {
   width: 48px;
   height: 48px;
   border: 5px solid #fff;
   border-bottom-color: transparent;
   border-radius: 50%;
   display: inline-block;
   box-sizing: border-box;
   animation: rotation 1s linear infinite;
}

@keyframes rotation {
   0% {
      transform: rotate(0deg);
   }
   100% {
      transform: rotate(360deg);
   }
}
</style>
