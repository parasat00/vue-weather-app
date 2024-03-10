<template>
 <div class="default">
  <slot></slot>
 </div>
</template>

<script>
 export default {
  
 }
</script>

<style scoped>
 .default {
  width: 100%;
  height: 380px;
  display: grid;
  place-items: center;
  font-size: 2rem;
  font-size: clamp(0.9rem, -0.567rem + 5.867vw, 2rem);
  text-align: center;
 }
</style>