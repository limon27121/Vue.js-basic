<script setup>
import { ref,onMounted} from 'vue'
import { Chart } from 'chart.js/auto';
let new_value1=ref();

let chart=null;
let datasets=[300, 50, 100];
const data = {
  labels: [
    'Red',
    'Blue',
    'Yellow',
  ],
  datasets: [{
    label: 'My First Dataset',
    data: [300, 50, 100],
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(255, 205, 86)',
      'rgb(0, 128, 0)',
      'rgb(255,0,0)',
      'rgb(128,128,0)'
    ],
    hoverOffset: 4
  }]
};
const config = {
  type: 'doughnut',
  data: data,
};
onMounted(()=>{
    const ctx=document.getElementById("myChart");
    chart=new Chart(ctx,config);
})

function add(){
    datasets.push(new_value1);
    chart.data.datasets[0].data=datasets;
    chart.update();
    new_value1.value='';
}
</script>

<template>
 <div>
  <canvas id="myChart"></canvas>
  <input type="text" v-model="new_value1">
  <button @click="add()">add value</button>
</div>

</template>