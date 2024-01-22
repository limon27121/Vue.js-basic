<script setup>
import { ref } from 'vue'
let click_details=ref(false)
let user=ref([])
let filter_user=ref([])
let country_name=ref()

//fetch all country details
async function fetchUsers() {
  try {
    let response = await fetch('https://restcountries.com/v3.1/all');
    let data = await response.json();
    user.value = data;
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchUsers()

//call specific country api using unique id
function find(id) {
  const url = `https://restcountries.com/v3.1/alpha/${id}`;
  async function fetchUsers1(url) {
    try {
      let response = await fetch(url);
      let data = await response.json();
      filter_user.value=data
    } catch (error) {
      console.error("Error:", error);
    }
  }
  fetchUsers1(url);
  click_details.value=true
}

//call click event methods to go to home page from country page 
function back(){
  click_details.value=false
}

//using filter according to input value from  the input form
const filterUsers = () => {
  if (country_name.value) {
    return user.value.filter((u1) => u1.name.official.toLowerCase().includes(country_name.value.toLowerCase()));
  }
   else {
    return user.value;
  }
};

//input form value clear
function clear(){
  country_name.value=""
}

</script>

<template>
<ul v-show="!click_details">
  <h1>World Tour</h1>
<input type="text" placeholder="country_name" v-model="country_name" class="input" >
  <button class="c1" @click="clear()">Clear</button>
  <div v-for="u1 in  filterUsers()" class="card">
  <p> Country name: {{ u1.name.official}}</p>
  <p>Capital name:
  <span v-for="(capital, index) in u1.capital" :key="index">
    {{ capital }}
  </span>
</p>
  <button @click="find(u1.cca2)">Details</button>
  </div>
</ul>

<div>
<h2>Country</h2>
<div v-show="click_details" class="details-container">
 
    <template v-for="user in filter_user" :key="user.cca2">
      <div class="user-details">
        <p class="country-name">Country Name: {{ user.name.common }}</p>
        <p class="capital">Capital: <span v-for="capital in user.capital" :key="capital">{{ capital }}</span></p>
        <img :src="user.flags.png" alt="Flag" class="flag">
        <p class="region">Region: {{ user.region }}</p>
        <p class="google-maps">Google Map: <a :href="user.maps.googleMaps" target="_blank">Country Maps</a></p>
        <button @click="back" class="back-button">Home page</button>
      </div>
    </template>
  </div>
</div>
</template>


<style scoped>
.card {
  border: 1px solid #ccc;
  border-radius: 8px;
  margin: 10px;
  padding: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: grey;
}

.card p {
  margin: 5px 0;
  color: black;
}

.card button {
  background-color: #007BFF;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}
.input{
  width: 150px;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
.c1{
  padding-left: 20px;
  margin-left: 20px;
  width: 130px;
  height: 40px;
}

.details-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: bisque;
  color: #007BFF;
}

.user-details {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 20px;
  margin: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.country-name {
  font-size: 18px;
  font-weight: bold;
}

.capital {
  margin-top: 10px;
}

.flag {
  max-width: 100%;
  margin-top: 10px;
}

.region {
  margin-top: 10px;
}

.google-maps {
  margin-top: 10px;
}

.back-button {
  background-color: #007BFF;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}
</style>
