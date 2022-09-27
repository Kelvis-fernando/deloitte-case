<template>
  <div class="app">
    <Nav />
    <div class="card-container">
      <Card />
    </div>
  </div>
</template>

<script setup>
import Card from "./components/Card.vue";
import Nav from "./components/Nav.vue";
</script>

<style scoped>
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 15px;
}
</style>
