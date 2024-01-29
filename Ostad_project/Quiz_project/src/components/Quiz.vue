<script setup>
import { ref } from 'vue';
const capitals=[];
const Saarc_countries = ref([
  { country: 'India', town: 'New Delhi' },
  { country: 'Pakistan', town: 'Islamabad' },
  { country: 'Bangladesh', town: 'Dhaka' },
  { country: 'Sri Lanka', town: 'Colombo' },
  { country: 'Nepal', town: 'Kathmandu' },
  { country: 'Bhutan', town: 'Thimphu' },
  { country: 'Maldives', town: 'Malé' },
  { country: 'Afghanistan', town: 'Kabul' },
]);

Saarc_countries.value.forEach(element => {
  capitals.push(element.town)
});

function get_random() {
    // return capitals.sort(() => Math.random() - 0.5);
    return capitals;
}


function get_score(){
    let score=0;
    Saarc_countries.value.forEach((c1)=>{
     if(c1.answer===c1.town){
        score++;
     }
   })
   return score;
}

</script>

  <template>
   
    <p>Your score: {{get_score()}}</p>
  <div>
    <div v-for="country in Saarc_countries" :key="country.town" class="card">
      <p class="p1">What is the capital of {{ country.country }}</p>
      <template v-for="(capital, index) in get_random()" :key="index">
        <div class="checkbox-wrapper">
            <input :name="country.country" type="radio" :value="capital" v-model="country.answer" />
            <label>{{ capital }}</label>
        </div>
      </template>
    </div>
  </div>
</template>


<style>
  .card {
    border: 1px solid #ddd;
    padding: 10px;
    margin: 10px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  
  }

  .checkbox-wrapper {
    margin-bottom: 8px;
    text-align: center;
    color: brown;
  }
  .p1{
    color: blue;
    text-transform: uppercase;
  }
</style>

