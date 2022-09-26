<template>
  <div class="card" v-for="responses in response" v-bind:key="responses">
    <img
      :src="responses.thumbnail.path + '.' + responses.thumbnail.extension"
      alt="pokemon"
      class="image"
    />
    <h4 class="name">{{ responses.name }}</h4>
  </div>
</template>

<script>
import axios from "axios";
import MD5 from "../utils/Md5";

// Neste caso seria ideal colocar as keys em um .env, porem decidi não colocar para que você possa subir o projeto e ver funcionando sem gerar nenhuma chave nova, mas fica este adendo.
const publicKey = "5a237863b3cc2061003cbbc4fe20dc06";
const privateKey = "fbf255068eccea6d0ef951b9f25626b57ab2fe72";

const ts = Number(new Date());
const hash = MD5(ts + privateKey + publicKey);
const baseUrl = "https://gateway.marvel.com/v1/public/characters?ts=";

export default {
  inheritAttrs: false,
  data() {
    return {
      response: [],
      imgValidation: "http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available",
    };
  },
  created: function () {
    axios.get(baseUrl + ts + "&apikey=" + publicKey + "&hash=" + hash).then((response) => {
      this.response = response.data.data.results;
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
  height: 30px;
  color: #fff;
}
</style>
