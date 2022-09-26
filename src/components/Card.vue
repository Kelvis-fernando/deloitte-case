<template>
  <div class="card" v-for="responses in response" v-bind:key="responses">
    <img
      :src="responses.thumbnail.path + '.' + responses.thumbnail.extension"
      alt="pokemon"
      class="image"
    />
    <h4>{{ responses.name }}</h4>
  </div>
</template>

<script>
import axios from "axios";
import MD5 from "../utils/Md5";

const ts = Number(new Date());

// Neste caso seria ideal colocar as keys em um .env, porem decidi não colocar para que você possa subir o projeto e ver funcionando sem gerar nenhuma chave nova, mas fica este adendo.
const publicKey = "5a237863b3cc2061003cbbc4fe20dc06";
const privateKey = "fbf255068eccea6d0ef951b9f25626b57ab2fe72";

const hash = MD5(ts + privateKey + publicKey);
const baseUrl = "https://gateway.marvel.com/v1/public/characters?ts=";

export default {
  inheritAttrs: false,
  data() {
    return {
      response: [],
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
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: rgb(155, 218, 158);
  margin: 5px;
  width: 200px;
  border-radius: 5px;
}
.card:hover {
  box-shadow: 2px 2px 3px rgb(136, 136, 136);
}

.image {
  background-color: #fff;
  border-radius: 50%;
  width: 100px;
}
</style>
