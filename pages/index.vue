<template>
  <div class="container px-4 mx-auto text-left">
    <h1 class="text-center">9996.</h1>
    <div
      class="w-full p-2 mt-2 overflow-scroll bg-white border-2 border-black border-solid wrapper-word h-base"
    >
      <div v-if="loading">loading</div>
      <div id="word" v-else class="w-full" v-html="word"></div>
    </div>
    <div class="flex items-center justify-center p-4">
      <button @click="getWord()" class="px-8 py-2 tracking-widest text-white bg-black">ACAK</button>
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
    const { data } = await axios.get("https://api-9996.herokuapp.com/api/v1");
    const text = data[0].texts.replace(/&nbsp;/g, " ");
    return { word: text };
  },
  methods: {
    async getWord() {
      axios.get("https://api-9996.herokuapp.com/api/v1").then(res => {
        this.word = res.data[0].texts.replace(/&nbsp;/g, " ");
      });
    },
    start() {
      this.loading = true;
    },
    finish() {
      this.loading = false;
    }
  }
};
</script>

<style>
body {
  @apply bg-orange-400;
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

.wrapper-word {
  box-shadow: 10px 10px 1px black;
}
</style>
