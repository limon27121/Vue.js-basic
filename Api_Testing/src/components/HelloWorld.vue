
<script setup>
import { ref } from 'vue';

let user = ref([]);
let input = ref("");

async function fetchUsers() {
  try {
    let response = await fetch('https://jsonplaceholder.typicode.com/users');
    let data = await response.json();
    user.value = data;
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchUsers();

const filterUsers = () => {
  if (input.value) {
    return user.value.filter((u1) => u1.name.toLowerCase().includes(input.value.toLowerCase()));
  } else {
    return user.value;
  }
};

function clear(){
  input.value=""
}
</script>

<template>
  <div>
    <input type="text" placeholder="search" v-model="input">
    <button @click="clear()">Clear</button>
    <ol>
      <li v-for="u1 in filterUsers()" :key="u1.id">
        <p>User Name: {{ u1.name }}</p>
        <p>User Mail: {{ u1.email }}</p>
        <p>Address: street {{u1.address.street}}, suite is: {{u1.address.suite}}, city is: {{u1.address.city}}</p>
        <p>Phone is: {{u1.phone }}</p>
        <p>Company Website: <a :href="u1.website" target="_blank">{{u1.company.name}}</a></p>
      </li>
    </ol>
  </div>
</template>

<style scoped>
/* Your styles here if needed */
</style>
