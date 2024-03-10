<template>
  <the-weather></the-weather>
</template>

<script>
  import TheWeather from '@/components/TheWeather';

  export default {
    components: {
      TheWeather
    }
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: rgba(0, 0, 0, 0.6);
}
#app {
  width: 100%;
  display: grid;
  place-items: center;
  font-family: "Roboto", sans-serif;
}
@media only screen and (max-width: 400px) {
#app {
  display: block;
  padding-top: 5px;
}
}
</style>