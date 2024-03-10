<template>
 <div class="weather__date">
  <div class="weather__date_date">{{ date.date }}</div>
  <div class="weather__date_time">{{ date.time }}</div>
 </div>
</template>

<script>
 export default {
  props: ['date']
 }
</script>

<style scoped>
 .weather__date {
  text-align: center;
  font-size: clamp(1.1rem, 0.225rem + 4vw, 1.5rem);
 }
 .weather__date_time {
  font-weight: bold;
  font-size: clamp(1.3rem, 0.4rem + 4.8vw, 1.6rem);
 }
</style>