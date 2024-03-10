<template>
 <div class="weather__main">
  <div :class="['weather__weather', `weather__weather_${weatherClass}`]"></div>
  <p class="weather__description">{{ description }}</p>
  <h2 class="weather__temp">{{ temp }}°C</h2>
  <div class="weather__place">{{ place }}</div>
 </div>
</template>

<script>
 export default {
  props: ['weatherClass', 'description', 'temp', 'place']
 }
</script>

<style scoped>
.weather__weather {
 width: 94px;
 height: 94px;
 margin: 0 auto 10px;
}
.weather__weather_sun {
 background: center / cover no-repeat url('@/assets/sun-icon.png');
}
.weather__weather_moon {
 background: center / cover no-repeat url('@/assets/moon-icon.png');
}
.weather__weather_rain {
 background: center / cover no-repeat url('@/assets/rain.png');
}
.weather__weather_snow {
 background: center / cover no-repeat url('@/assets/snow.png');
}
.weather__weather_atmosphere {
 background: center / cover no-repeat url('@/assets/atmosphere.png');
}
.weather__weather_thunderstorm {
 background: center / cover no-repeat url('@/assets/thunderstorm.png');
}
.weather__weather_cloud_day {
 background: center / cover no-repeat url('@/assets/cloudy-day.png');
}
.weather__weather_cloud_night {
 background: center / cover no-repeat url('@/assets/cloudy-night.png');
}

.weather__temp {
 font-size: clamp(2.2rem, -1rem + 12.8vw, 3rem);
 margin-bottom: 20px;
}
.weather__place {
 font-size: clamp(1.3rem, -0.3rem + 6.4vw, 1.7rem);
}
@media only screen and (max-width: 500px) {
 .weather__weather {
  width: 82px;
  height: 82px;
 }
}
</style>