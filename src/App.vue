<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import Bmi from './components/Bmi.vue';
import './assets/styles/style.css';

// const activity = ref({});
// const result = ref({});

// const fetchData = async () => {
//   const options = {
//     method: 'GET',
//     url: 'https://fitness-calculator.p.rapidapi.com/burnedcalorie',
//     params: {
//       activityid: 'bi_1',
//       activitymin: '25',
//       weight: '75',
//     },
//     headers: {
//       'X-RapidAPI-Key': 'your-api-key',
//       'X-RapidAPI-Host': 'fitness-calculator.p.rapidapi.com',
//     },
//   };

//   try {
//     const response = await axios.request(options);
//     const responseData = response.data || {};
    
//     activity.value = responseData.activity || {};
    
//     result.value = {
//       calories_burned: responseData.data.burnedCalorie,
//       unit: responseData.data.unit,
//     };
    
//     console.log(responseData);
//   } catch (error) {
//     console.error(error);
//   }
// };

// onMounted(() => {
//   fetchData();
// });
</script>

<template>
  <div class="container">
    <!-- <header>
      <h2>Wywołaj API dla ilości spalonych kalorii</h2>
    </header>

    <div class="data">
      <p>ID aktywności: {{ result.id }}</p>
      <p>Nazwa aktywności: {{ activity.name }}</p>
      <p>Spalone kalorie: {{ result.calories_burned }} {{ result.unit }}</p>
    </div> -->
    
    <Bmi/>
  </div>
</template>

<style scoped>
.container {
  background: grey;
  padding: 20px;

  .data {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }
}
</style>
