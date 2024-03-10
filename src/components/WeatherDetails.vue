<template>
 <section class="weather__details">
  <weather-date :date="date" />

  <weather-main 
   :weather-class="weatherClass"
   :description="description"
   :temp="temp"
   :place="place"
  />
  
  <weather-more :humidity="humidity" :wind-speed="windSpeed"/>
 </section>
</template>

<script>
 import WeatherDate from '@/components/WeatherDate';
 import WeatherMore from '@/components/WeatherMore';
 import WeatherMain from '@/components/WeatherMain';

 export default {
  components: {
   WeatherDate,
   WeatherMore,
   WeatherMain
  },
  props: ['place', 'weather', 'description', 'temp', 'date', 'humidity', 'windSpeed', 'weatherClass'],
 }
</script>

<style>
.weather__details {
 width: 100%;
 height: 70vh;
 display: flex;
 flex-direction: column;
 align-items: center;
 justify-content: space-between;
 text-align: center;
 padding: 40px 0 0;
}
.weather__details>*:not(:last-child) {
 filter: drop-shadow(4px 4px 1px rgba(0, 0, 0, 0.25));
}
@media only screen and (max-width: 400px) {
 .weather__details {
  padding-top: 20px;
  height: 380px;
 }
}
</style>