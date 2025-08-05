<template>
   <div class="contacer p-4">
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
});

onMounted(() => {
   loadDestination();
});

function loadDestination() {
   axios.get("http://localhost:3000/destination").then((response) => {
      console.log(response.data);
      destinationObj.destinationList = response.data;
   });
}
</script>
