<script setup>
import { ref } from 'vue';
import axios from 'axios';

const age = ref(25);
const weight = ref(70);
const height = ref(170);
const bmiResult = ref(null);
let responseCode = ref(200);
let errorMessage = ref("");

const calculateBMI = async () => {
  const options = {
    method: 'GET',
    url: 'https://fitness-calculator.p.rapidapi.com/bmi',
    params: {
      age: age.value,
      weight: weight.value,
      height: height.value,
    },
    headers: {
      'X-RapidAPI-Key': '2640467764msh3f6901d913f0faep1dbe1djsn85c1bf767f63',
      'X-RapidAPI-Host': 'fitness-calculator.p.rapidapi.com',
    },
  };

  try {
    const response = await axios.request(options);
    bmiResult.value = response.data.data || null;

    console.log(response.data.data);
    console.log("Status code: ", response.data.status_code);
    responseCode = 200;

  } 
  catch (error) {
    if (error.response && error.response.status === 422) {
      responseCode = 422;
	  console.log("Status Code:", error.response.status);
	  errorMessage = "Nieprawidlowe dane wejściowe! Wiek [1;80], waga [40;160], wzrost [130;230]";
    }
	else {
      errorMessage = "Wystąpił błąd. Spróbuj ponownie.";
    }
	alert(errorMessage);
  }
};
</script>

<template>
  	<div class="bmi-calculator">
		<h2>Oblicz swoje BMI</h2>
        <div class="grid">
            <div class="input-container">
                <label for="age">Wiek:</label>
                <input type="number" id="ageInput" min="1" max="80" v-model="age" disabled/>
                <input type="range" id="ageRange" min="1" max="80" v-model="age">
            </div>
            
            <div class="input-container">
                <label for="weight">Waga (kg):</label>
                <input type="number" id="weightInput" min="40" max="160" v-model="weight" disabled/>
                <input type="range" id="weightRange" min="40" max="160" v-model="weight">
            </div>
            
            <div class="input-container">
                <label for="height">Wzrost (cm):</label>
                <input type="number" id="heightInput" min="130" max="230" v-model="height" disabled/>
                <input type="range" id="heightRange" min="130" max="230" v-model="height">
            </div>
        </div>
		
		
		<button @click="calculateBMI">Oblicz BMI</button>
		
		<div class="no-data">
			<p>{{errorMessage}}</p>
		</div>
		
		<div v-if="bmiResult !== null" class="result-container">
			<h3><u>Wynik Twojego BMI:</u></h3>
			<p><b>BMI:</b> {{ bmiResult.bmi }}</p>
			<p><b>Zakres zdrowego BMI:</b> {{ bmiResult.healthy_bmi_range }}</p>
			<p><b>Zdrowie:</b> {{ bmiResult.health }}</p>
		</div>
    </div>
</template>

<style scoped>
  template {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  .bmi-calculator {
    max-width: 400px;
    margin: 0 auto;
    border: 1px solid white;
    padding: 10px;
  }

  h2, h3 {
    margin: 8px;
    text-align: center;
  }

  .input-container {
    margin-bottom: 15px;
    display: flex;
    align-items: center;
  }

  input:disabled{
    color: black;
    width: 15%;
  }

  button {
    padding: 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    cursor: pointer;
    width: 100%;
  }

  button:hover {
    background-color: #004ea1;
  }

  .result-container {
    margin-top: 20px;
    border: 1px solid #ccc;
    padding: 10px;
  }

  .no-data {
    margin-top: 20px;
    color: #ff0000;
    text-align: center;
    font-weight: bold;
  }
</style>
