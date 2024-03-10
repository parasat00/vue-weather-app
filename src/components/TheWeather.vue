<template>
 <div :class="['weather', `weather_${weatherClass}`]">
  <the-search @weather-info="getWeatherInfo"/>
  <weather-details 
   v-if="weather_info"
   :place="weather_info.place" 
   :temp="weather_info.temperature" 
   :weather="weather_info.weather"
   :description="weather_info.description"
   :date="weather_info.date"
   :humidity="weather_info.humidity"
   :wind-speed="weather_info.windSpeed"
   :weather-class="weatherClass"/>
  <default-component v-else>Please enter city name to know weather...</default-component>
 </div>
</template>

<script>
import TheSearch from '@/components/TheSearch';
import WeatherDetails from '@/components/WeatherDetails';
import DefaultComponent from '@/components/DefaultComponent';

 export default {
  components: {
   TheSearch,
   WeatherDetails,
   DefaultComponent
  },
  data() {
   return {
    weather_info: null,
    weatherClass: 'default'
   };
  },
  methods: {
   getWeatherClass() {
    let output = '';
    const weather_name = this.weather_info.weather.toLowerCase();
    const hour = this.weather_info.date.time_24;

    if(weather_name === 'clear') {
     output = hour > 5 && hour < 21 ? 'sun' : 'moon';
    }
    else if(weather_name === 'clouds') {
     output = hour > 5 && hour < 21 ? 'cloud_day' : 'cloud_night';
    }
    else if(weather_name === 'drizzle') {
     output = 'rain';
    }else if(this.weather_info.id[0] === '7') {
     output = 'atmosphere';
    }

    
    if(output === '') {
     output = weather_name;
    }
    
    return output;
   },
   getWeatherInfo(obj) {
    this.weather_info = obj;
    this.weatherClass = this.getWeatherClass();
   },
  }
 }
</script>

<style scoped>
.weather {
  padding: 40px 45px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border-radius: 18px;
  border: none;
  color: #fff;
  width: 500px;
}
.weather_default {
 background-color: #444;
}
.weather_sun {
  background-color: rgba(247, 214, 116, 1);
  background-image: linear-gradient(45deg, rgba(247, 214, 116, 1), rgba(242, 164, 131, 1));
}
.weather_moon {
  background-image: linear-gradient(45deg, rgba(116, 216, 247, 1), rgba(1, 9, 222, 1));
}
.weather_cloud_day {
 background-image: linear-gradient(45deg, rgba(104, 179, 208, 1), rgba(61, 171, 205, 1));
}
.weather_cloud_night {
 background-image: linear-gradient(45deg, rgba(247, 116, 242, 0.72), rgba(7, 47, 188, 1));
}
.weather_thunderstorm {
 background-image: linear-gradient(45deg, rgba(144, 90, 212, 1), rgba(51, 48, 165, 1));
}
.weather_rain {
 background-image: linear-gradient(45deg, rgba(117, 215, 237, 1), rgba(11, 207, 172, 1));
}
.weather_snow {
 background-image: linear-gradient(45deg, rgba(117, 237, 208, 1), rgba(11, 67, 207, 1));
}
.weather_atmosphere {
 background-image: linear-gradient(45deg, rgba(119, 240, 211, 1), rgba(9, 130, 167, 1));
}

@media only screen and (max-width: 500px) {
  .weather {
    width: calc(100% - 20px);
    margin: 0 10px;
    padding: 40px 25px;
  }
}
</style>