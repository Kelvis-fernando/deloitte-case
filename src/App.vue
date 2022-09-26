<script setup>
import Card from "./components/Card.vue";
import Nav from "./components/Nav.vue";
</script>

<template>
  <div class="app">
    <Nav />
    <div class="card-container">
      <Card />
      <Card />
      <Card />
      <Card />
      <Card />
      <Card />
      <Card />
      <Card />
      <Card />
    </div>
  </div>
</template>

<style scoped>
.app {
  display: flex;
}

.card-container {
  display: grid;
  grid-template-columns: auto auto auto auto auto auto;
  grid-template-rows: 150px 150px 150px 150px;
  margin: 15px;
}
</style>
