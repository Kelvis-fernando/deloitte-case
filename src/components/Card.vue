<template>
  <div class="card" v-for="responses in response" v-bind:key="responses">
    <img :src="responses.image" alt="capa do filme" class="image" />
    <h4 class="name">{{ responses.titleOriginal }}</h4>
  </div>
  <footer>
    <div ref="infinitescrolltrigger" id="scoll-trigger"></div>
    <div class="circle-loader" v-if="showloader"></div>
  </footer>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      response: [],
      currentPage: 1,
      maxPerPage: 24,
      totalResults: 240,
      showloader: false,
      options: {
        method: "GET",
        url: `https://movies-app1.p.rapidapi.com/api/movies?page=${this.currentPage}`,
        params: { page: "1", limit: "24" },
        headers: {
          "X-RapidAPI-Key": "ad1a634496mshcc6365583085806p15f9bdjsn07f41c943008",
          "X-RapidAPI-Host": "movies-app1.p.rapidapi.com",
        },
      },
    };
  },
  created: async function () {
    await axios.request(this.options).then((response) => {
      this.response.push(...response.data.results);
    });
  },
  computed: {
    pageCount() {
      return Math.ceil(this.totalResults / this.maxPerPage);
    },
    pageOffset() {
      return this.maxPerPage * this.currentPage;
    },
  },
  methods: {
    scrollTrigger() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.intersectionRatio > 0 && this.currentPage < this.pageCount) {
            this.showloader = true;
            this.currentPage += 1;
            this.showloader = false;

            axios
              .get(`https://movies-app1.p.rapidapi.com/api/movies?page=${this.currentPage}`, {
                headers: {
                  "X-RapidAPI-Key": "ad1a634496mshcc6365583085806p15f9bdjsn07f41c943008",
                  "X-RapidAPI-Host": "movies-app1.p.rapidapi.com",
                },
              })
              .then((response) => {
                this.response.push(...response.data.results);
              });
          }
        });
      });
      observer.observe(this.$refs.infinitescrolltrigger);
    },
  },
  mounted() {
    this.scrollTrigger();
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

.circle-loader {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 5px solid rgba(255, 255, 255, 0.2);
  border-top: 5px solid #fff;
  animation: animate 1.5s infinite linear;
}

@keyframes animate {
  0% {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  100% {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}
</style>
