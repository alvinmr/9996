<template>
  <div class="container px-4 mx-auto text-left">
    <h1 class="text-center">9996.</h1>
    <div
      class="w-full p-2 mt-2 overflow-scroll bg-white border-2 border-black border-solid  wrapper-word"
    >
      <div v-if="loading">Sedang memuat....</div>
      <div id="word" v-else class="w-full" v-html="word"></div>
    </div>
    <div class="flex justify-center mt-5">
      <button
        class="px-8 py-2 tracking-widest text-white bg-black"
        @click="goToPrev()"
      >
        KEMBALI
      </button>
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
    const value = `; ${document.cookie}`;
    const parts = value.split(`; word=`);
    return { word: parts.length === 2 ? parts.pop().split(";").shift() : "" };
  },
  methods: {
    getCookie(name) {
      const value = `; ${document.cookie}`;
      const parts = value.split(`; ${name}=`);
      if (parts.length === 2) return parts.pop().split(";").shift();
    },
    goToPrev() {
      this.$router.go(-1);
    },
  },
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
</style>

<style scoped>
.wrapper-word {
  box-shadow: 10px 10px 1px black;
  height: 86vh;
}
</style>
