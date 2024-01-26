<script setup>
import axios from 'axios';

const options = {
    method: 'GET',
    url: 'https://fitness-calculator.p.rapidapi.com/burnedcalorie',
    params: {
        activityid: 'bi_1',
        activitymin: '25',
        weight: '75'
    },
    headers: {
        'X-RapidAPI-Key': 'your-api-key',
        'X-RapidAPI-Host': 'fitness-calculator.p.rapidapi.com'
    }
};

let activity = {};
let result = {};

try {
    const response = await axios.request(options);
    activity = response.data.activity || {};
    result = response.data.result || {};
    console.log(response.data);
} 
catch (error) {
    console.error(error);
}
</script>

<template>
    <div>
        <header>
            <h2>Call API for calories amount</h2>
        </header>
        <div>
            <p>Activity ID: {{ activity.id }}</p>
            <p>Activity Name: {{ activity.name }}</p>
            <p>Calories Burned: {{ result.calories_burned }}</p>
        </div>
    </div>
</template>

<style scoped>

</style>
