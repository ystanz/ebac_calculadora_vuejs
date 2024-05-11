<script setup>
import Header from './components/Header.vue'
import Calculator from './components/Calculator.vue'

  
</script>

<template>
<div data-bs-theme="dark" class="container">
  <Header></Header>
  <Calculator></Calculator>
</div>
</template>

<style scoped>
  .container {
    max-width: 640px;
    width: 100%;
  }
</style>
