<script setup>
import { ref } from 'vue'
let user=ref([])
let filter_user=ref([])
let phone=ref("")
let click_details=ref(false)
async function fetchUsers() {
  try {
    let response = await fetch('https://openapi.programming-hero.com/api/phones?search=iphone');
    let data = await response.json();
    user.value = data.data;
  } catch (error) {
    console.error("Error:", error);
  }
}
fetchUsers()

const filterUsers = () => {
  if (phone.value) {
    return user.value.filter((u1) => u1.phone_name.toLowerCase().replace(/\s/g, '').includes(phone.value.toLowerCase()));
  }
   else {
    return user.value;
  }
};
function clear(){
    phone.value=""
}

async function find(id) {
  const url = `https://openapi.programming-hero.com/api/phone/${id}`;

  async function fetchUsers1(url) {
    try {
      let response = await fetch(url);
      let data = await response.json();
      filter_user.value = data.data;
      console.log(filter_user.value);
    } catch (error) {
      console.error("Error:", error);
    }
  }

  // Call the fetchUsers1 function with the specified URL
   fetchUsers1(url);
   click_details.value=true

}

function back(){
    click_details.value=false
}



</script>

<template>
    <div v-if="!click_details">
    <h1>Apple Store</h1>
    <input type="text" placeholder="Phone_name" v-model="phone">
    <button @click="clear()" class="b1">clear</button>
    <div class="body">
    <div class="card" v-for="u1 in filterUsers()" :key="u1">
  <img :src="u1.image" alt="Avatar" style="width:100%">
  <div class="container">
    <h4><b>{{ u1.brand }}</b></h4>
    <p>{{ u1.phone_name }}</p>
    <button @click="find(u1.slug)">Click</button>
  </div>
</div>
</div>
</div>

<div v-if="click_details">
<div class="body">
    <div class="card">
  <img :src="filter_user.image" alt="Avatar" style="width:50%">
  <div class="container">
    <h4 style='padding-left: 30px;'><b>{{ filter_user.name }}</b></h4>
     <ul>
     <h2>Details</h2>
     <div style="text-align: left;">
     <li>{{ filter_user.mainFeatures.chipSet }}</li>
     <li>{{filter_user.mainFeatures.displaySize }}</li>
     <li>{{ filter_user.mainFeatures.memory }}</li>
     <li>{{ filter_user.mainFeatures.storage }}</li>
     <li>{{ filter_user.releaseDate }}</li>
    </div>
     </ul>
  </div>
</div>
</div>
<button @click="back()">back</button>
</div>

</template>

<style scoped>
.body{
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 20px;
    display: flex;
    flex-wrap: wrap;
}

.card {
  /* Add shadows to create the "card" effect */
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  margin: 20px;
  background-color: gray;
}

/* On mouse-over, add a deeper shadow */
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
  color:blue;
}
.b1{
    margin-left: 10px;
}
</style>