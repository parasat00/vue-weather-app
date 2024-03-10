<template>
 <div class="weather__more">
  <additional-stats img="humidity" title="Humidity" :val="`${humidity}%`"/>
  <additional-stats img="wind" title="Wind Speed" :val="windSpeed"/>
 </div>
</template>

<script>
 import AdditionalStats from '@/components/AdditionalStats.vue';

 export default {
  props: ['humidity','windSpeed'],
  components: {
   AdditionalStats
  }
 }
</script>

<style scoped>
.weather__more {
 width: 100%;
 display: flex;
 align-items: center;
 justify-content: space-between;
}
.weather__more_block {
 display: flex;
}
</style>