<template>
 <div class="add-stat weather__stat">
  <img :src="require(`@/assets/${img}.png`)" :alt="title" class="add-stat__img">
  <div class="add-stat__block">
   <h3 class="add-stat__header">{{ val }}</h3>
   <div class="add-stat__title">{{ title }}</div>
  </div>
 </div>
</template>

<script>
 export default {
  props: ['img','title', 'val']
 }
</script>

<style scoped>
.weather__stat {
 display: flex;
 align-items: center;
 gap: 10px;
}
.add-stat__block {
 text-align: left;
}
.add-stat__header {
 font-weight: 400;
 font-size: clamp(1.2rem, -0.4rem + 8vw, 1.6rem);
}
.add-stat__title {
 font-size: clamp(0.7rem, 0.3rem + 2vw, 0.8rem);
}

@media only screen and (max-width: 400px) {
 .add-stat__img {
  width: 40px;
 }
}
</style>