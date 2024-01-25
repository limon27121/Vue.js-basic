<script setup>
import { ref } from 'vue'

let textInputValue=ref("");
let checkboxValues=ref([]);
let radioValue=ref("");
let selectedOption=ref();
</script>

<template>
<div>
    <label for="textInput">Text Input:</label>
    <input type="text" id="textInput" v-model="textInputValue" />
    <br>
    <p>{{ textInputValue}}</p>
</div>
<div>
    <label for="checkbox1">Checkbox1:</label>
    <input type="checkbox" id="checkbox1" v-model="checkboxValues[0]" />

    <label for="checkbox2">Checkbox2:</label>
    <input type="checkbox" id="checkbox2" v-model="checkboxValues[1]" />

    <p>Checkbox1 Value: {{ checkboxValues[0] }}</p>
    <p>Checkbox2 Value: {{ checkboxValues[1] }}</p>
  </div>

<div>
    <label>Radio Buttons:</label>
    <div>
      <input type="radio" id="radioOption1" value="rice" v-model="radioValue" />
      <label for="radioOption1">Rice</label>

      <input type="radio" id="radioOption2" value="Egg" v-model="radioValue" />
      <label for="radioOption2">Egg</label>
    </div>
    <p>{{ radioValue }}</p>
</div>
<div>
    <label for="selectBox">Select Box:</label>
    <select id="selectBox" v-model="selectedOption">
      <option value="option1">Option 1</option>
      <option value="option2">Option 2</option>
      <option value="option3">Option 3</option>
    </select>

    <p>Selected Option: {{ selectedOption }}</p>
</div>
</template>