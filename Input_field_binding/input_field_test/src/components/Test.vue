<script setup>
import { ref,reactive } from 'vue'
let url="images.app.goo.gl/vUS7jJPTxvJD7Q5v6"
let selected=ref([])
let check=ref();
let persons=reactive([
    {name:"limon",age:26,work:"developer"},
    {name:"fahim",age:25,work:"tester"}
])
let color=ref();
function get_style(){
    return{
    backgroundColor: color.value,
    }
}
</script>
<template>
    <select v-model="selected">
  <option v-for="person in persons" :value="{ age: person.age, name: person.name }">
    {{ person.name }}
  </option>
</select>
<p>name is:{{ selected.name }}</p>
<p>age is:{{ selected.age }}</p>

<div>
<label for="">enter color</label> <input type="text" v-model="color">
</div>
<div :style="get_style()">
<p :style="{ color: color === 'white' ? 'black' : 'white' }">here is the section</p>
</div>

<input type="radio" id="one" :value="true" v-model="check" />
<label for="one">One</label>

<input type="radio" id="two" :value="false" v-model="check" />
<label for="two">Two</label>

<div>
 <img :src="url" alt="No Image">
</div>
</template>
<style scoped>
</style>