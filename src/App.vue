<template>
  <div class="app">
    <div class="nav">
      <img src="./assets/logo.png" alt="Logo" height="30" width="40" />
    </div>
    <div class="card-container">
      <Card />
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";

export default {
  components: {
    Card,
  },
};
</script>

<style scoped>
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 15px;
}

.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #000;
  height: 50px;
  width: 100%;
}

.search {
  border: none;
  height: 30px;
  width: 220px;
  padding-left: 10px;
  margin-right: 10px;
  border-radius: 5px;
}
</style>
