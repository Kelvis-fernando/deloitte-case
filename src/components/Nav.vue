<template>
  <div class="nav">
    <img src="../assets/logo.png" alt="Logo" height="30" width="40" />
    <input v-model="search" class="search" type="text" placeholder="Procure pelo seu heroi" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  computed: {
    filteredHeroes: () => {
      return this.heroes.filter((hero) => {
        return hero.name.match(this.search);
      });
    },
  },
  props: {
    heroes: [],
  },
};
</script>

<style scoped>
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
