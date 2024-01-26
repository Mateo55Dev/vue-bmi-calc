<script setup>
  import { ref } from 'vue';
  import axios from 'axios';
  
  const age = ref(25);
  const weight = ref(65);
  const height = ref(180);
  const bmiResult = ref(null);
  let isError = ref(false);
  
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
        'X-RapidAPI-Key': 'your-api-key',
        'X-RapidAPI-Host': 'fitness-calculator.p.rapidapi.com',
      },
    };
  
    try {
      const response = await axios.request(options);
      bmiResult.value = response.data.data || null;
      console.log(response.data.data);
      console.log("Status code: ",response.data.status_code);
      isError = false;
    } catch (error) {
      isError = true;
      console.error(error);
    }
  };
  </script>

  <template>
    <div class="bmi-calculator">
        <h2>Oblicz swoje BMI</h2>
        <div class="input-container">
        <label for="age">Wiek:</label>
        <input v-model="age" type="number" id="age" min="1" max="80"/>
        </div>
        <div class="input-container">
        <label for="weight">Waga (kg):</label>
        <input v-model="weight" type="number" id="weight" min="40" max="160"/>
        </div>
        <div class="input-container">
        <label for="height">Wzrost (cm):</label>
        <input v-model="height" type="number" id="height" min="130" height="230"/>
        </div>
        <button @click="calculateBMI">Oblicz BMI</button>
        
        <div class="result">
            <div v-if="bmiResult !== null" class="result-container">
            <h3>Wynik BMI:</h3>
            <p><strong>BMI:</strong> {{ bmiResult.bmi }}</p>
            <p><strong>Zakres zdrowego BMI:</strong> {{ bmiResult.healthy_bmi_range }}</p>
            <p><strong>Zdrowie:</strong> {{ bmiResult.health }}</p>
        </div>

        <div v-else class="no-data">
          <p v-if="isError">Brak danych BMI</p>
        </div>
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

    h2{
      margin: 8px;
      text-align: center;  
    }
  
  .input-container {
    margin-bottom: 15px;
  }
  
  button {
    padding: 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    cursor: pointer;
    width: 100%;
  }

  button:hover{
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
    font-weight: bold
  }
  </style>
  