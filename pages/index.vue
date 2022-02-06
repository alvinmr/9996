<template>
  <div class="container px-4 mx-auto text-left">
    <h1 class="text-center">9996.</h1>
    <div
      class="w-full p-2 mt-2 overflow-scroll bg-white border-2 border-black border-solid  wrapper-word"
    >
      <div v-if="loading">Sedang memuat....</div>
      <div id="word" v-else class="w-full" v-html="word"></div>
    </div>
    <div class="flex items-center justify-center p-4">
      <div>
        <button
          @click="goToSaved()"
          class="px-8 py-2 mr-5 tracking-widest text-black bg-white"
        >
          SAVED
        </button>
      </div>
      <div>
        <button
          v-if="!loading"
          @click="getWord()"
          class="px-8 py-2 tracking-widest text-white bg-black"
        >
          ACAK
        </button>
        <button v-else class="px-8 py-2 tracking-widest text-white bg-black">
          MEMUAT
        </button>
      </div>
      <div>
        <button
          @click="saveWord()"
          class="px-2 ml-5 text-red-600 bg-white rounded-full"
        >
          ♥
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return { word: "", loading: false };
  },
  async asyncData({ params }) {
    const { data } = await axios.get("http://localhost:8000/api/v1");
    const text = data[0].texts.replace(/&nbsp;/g, " ");
    return { word: text };
  },
  methods: {
    async getWord() {
      this.loading = true;
      axios.get("http://localhost:8000/api/v1").then((res) => {
        this.word = res.data[0].texts.replace(/&nbsp;/g, " ");
        this.loading = false;
      });
    },
    async saveWord() {
      const word = this.word;
      const wordArray = JSON.parse(localStorage.getItem("word"));
      if (wordArray) {
        wordArray.push(word);
        localStorage.setItem("word", JSON.stringify(wordArray));
      } else {
        localStorage.setItem("word", JSON.stringify([word]));
      }
    },
    async goToSaved() {
      this.$router.push("/saved");
    },
  },
};
</script>

<style>
body {
  @apply bg-orange-400;
  background-color: orange;
}
* {
  font-family: "Roboto Mono";
}
::-webkit-scrollbar {
  display: none;
}
a {
  display: none;
}
</style>

<style scoped>
.wrapper-word {
  box-shadow: 10px 10px 1px black;
  height: 86vh;
}
</style>
