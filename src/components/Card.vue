<template>
  <div class="card" v-for="responses in response" v-bind:key="responses">
    <img :src="responses.image" alt="pokemon" class="image" />
    <h4 class="name">{{ responses.titleOriginal }}</h4>
  </div>
</template>

<script>
import axios from "axios";

const options = {
  method: "GET",
  url: "https://movies-app1.p.rapidapi.com/api/movies",
  params: { page: "1", limit: "24" },
  headers: {
    "X-RapidAPI-Key": "ad1a634496mshcc6365583085806p15f9bdjsn07f41c943008",
    "X-RapidAPI-Host": "movies-app1.p.rapidapi.com",
  },
};

export default {
  inheritAttrs: false,
  data() {
    return {
      response: [],
    };
  },
  created: function () {
    axios.request(options).then((response) => {
      this.response = response.data.results;
    });
  },
};
</script>

<style scoped>
.card {
  position: relative;
  display: flex;
  align-items: center;
  background: #999;
  margin: 5px;
  width: 200px;
  border-radius: 15px;
}
.card:hover {
  box-shadow: 2px 2px 3px rgb(136, 136, 136);
}

.image {
  width: 100%;
  height: 100%;
}

.name {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  bottom: 0;
  background-color: rgba(5, 5, 5, 0.8);
  width: 100%;
  height: 50px;
  color: #fff;
  text-align: center;
}
</style>
