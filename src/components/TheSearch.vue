<template>
 <div>
  <form @submit.prevent="searchWeather" class="search weather__search">
   <input type="text" 
    name="searchText" 
    id="searchText" 
    v-model.trim="searchText" 
    :class="['search__input', {'search__input_invalid' : !inputValid}]" 
    @blur="validate"
    placeholder="SEARCH CITY">
   <button class="search__btn"><img src="@/assets/search-icon.png" alt="search"></button>
  </form>
  <div class="weather__warn">
   <p v-show="!inputValid">{{ warningText }}</p>
  </div>
  
 </div>
</template>

<script>
 const addTh = (day) => {
  const remain = day % 10;
  return remain === 1 ? 'st' : remain === 2 ? 'nd' : remain === 3 ? 'rd' : 'th';
 }
 const formatHour = (hour, minute) => {
  const division = Math.floor(hour / 12);
  const remain = hour % 12;
  minute = minute < 10 ? `0${minute}` : minute;
  return division === 0 ? `${hour}:${minute} am` : remain === 0 ? `12:${minute}pm` : `${hour}:${minute}pm`;
 }
 const getLocalDate = (timezone) => {
  const weekDays = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  const monthNames = ['december', 'january', 'february', 'march', 'april', 'may', 'june', 'july', 'august', 'september', 'october', 'november'];
  const utc = new Date(new Date().toUTCString().substring(0, 25)).getTime();
  const localDate = new Date(utc + (timezone * 1000));
  const out_date = `${weekDays[localDate.getDay()]}, ${localDate.getDate()}${addTh(localDate.getDate())} ${monthNames[localDate.getMonth()]}`;
  const out_time = formatHour(localDate.getHours(), localDate.getMinutes());
  return {date: out_date, time: out_time, time_24:localDate.getHours()};
 }
 export default {
  emits: ['weather-info'],
  data() {
   return {
    searchText: '',
    api_key: '9b4ef6982a1a9fa186c12147196c5541',
    inputValid: true,
    warningText: null
   };
  },
  methods: {
   validate() {
    this.inputValid = !this.searchText === '';
    this.warningText = this.searchText === '' ? 'Empty input. Enter something...' : 'Invalid Input';
    console.log()
   },
   searchWeather() {
    if(this.searchText === '') {
     this.validate();
     return;
    }
    this.inputValid = true;
    fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.searchText}&appid=${this.api_key}&units=metric`)
    .then(response => {
     if(response.ok) {
      return response.json();
     }else {
      throw new Error('Invalid Input');
     }
    }).then(data => {
     const obj = {
      id: data.weather[0].id + '',
      place: data.name,
      weather: data.weather[0].main,
      description: data.weather[0].description,
      temperature: Math.floor(data.main.temp),
      humidity: data.main.humidity,
      windSpeed: data.wind.speed,
      date: getLocalDate(data.timezone)
     }
     this.$emit('weather-info', obj);
    }).catch((error) => {
     this.inputValid = false;
     this.warningText = error.message;
    });
    
    this.searchText = '';
   }
  }
 }
</script>

<style scoped>
 .search {
  display: flex;
  align-items: center;
  gap: 10px;
 }
 .search__input{
  padding: 10px 26px 8px;
  border-radius: 29px;
  color: #7d7d7d;
  font-size: clamp(0.8rem, 0.127rem + 4.308vw, 1.5rem);
  border: 3px solid transparent;
 }
 .search__btn {
  width: 55px;
  height: 55px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  cursor: pointer;
  border: none;
 }
 .search__btn>*{
  pointer-events: none;
 }
 .search__input, 
 .search__btn {
  background-color: #f7f7f7;
  outline: none;
  filter: drop-shadow(4px 4px 0 rgba(0, 0, 0, 0.25));
 }
 .search__input_invalid {
  border: 3px solid red;
  color: red;
 }
 .weather__warn {
  padding-left: 15px;
  color: red;
  height: 20px;
 }
 @media only screen and (max-width: 500px) {
  .search__input {
   padding: 10px 10px 8px 20px;
  }
  .search__btn {
   width: 45px;
   height: 45px;
  }
  .weather__warn {
   margin-top: 5px;
   padding-left: 10px;
   font-size: 0.8rem;
  }
}
@media only screen and (max-width: 400px) {
 .search__btn {
  display: none;
 }
}
</style>