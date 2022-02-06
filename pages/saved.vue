<template>
  <div class="px-4 mx-auto text-left">
    <h1 class="text-center">9996.</h1>
    <div>
      <!-- Make card for list blog -->
      <div v-for="(word, index) in words" :key="word.id" class="flex mt-5">
        <div
          class="w-full p-2 overflow-hidden bg-white border-2 border-black border-solid cursor-pointer  hover:text-white hover:bg-gray-700 wrapper-word"
        >
          <div v-html="word" @click="getWord(word)"></div>
        </div>
        <div>
          <button
            class="min-h-full p-2 bg-black hover:bg-white"
            @click="deleteItem(index)"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="red"
            >
              <path
                d="M3 6v18h18v-18h-18zm5 14c0 .552-.448 1-1 1s-1-.448-1-1v-10c0-.552.448-1 1-1s1 .448 1 1v10zm5 0c0 .552-.448 1-1 1s-1-.448-1-1v-10c0-.552.448-1 1-1s1 .448 1 1v10zm5 0c0 .552-.448 1-1 1s-1-.448-1-1v-10c0-.552.448-1 1-1s1 .448 1 1v10zm4-18v2h-20v-2h5.711c.9 0 1.631-1.099 1.631-2h5.315c0 .901.73 2 1.631 2h5.712z"
              />
            </svg>
          </button>
        </div>
      </div>
      <div class="flex justify-center mt-5">
        <button
          @click="goHome()"
          class="px-8 py-2 tracking-widest text-white bg-black"
        >
          BERANDA
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return { words: [] };
  },
  async asyncData({ params }) {
    // get data from localstorage
    const words = JSON.parse(localStorage.getItem("word"));
    return { words };
  },
  methods: {
    deleteItem(indexWord) {
      // delete item data from array localstorage
      const words = JSON.parse(localStorage.getItem("word"));
      const index = words.indexOf(indexWord);
      words.splice(index, 1);
      localStorage.setItem("word", JSON.stringify(words));
      this.words = JSON.parse(localStorage.getItem("word"));
    },
    getWord(word) {
      // set item into cookie
      document.cookie = "word=" + word;
      this.$router.push({ path: "/show" });
    },
    goHome() {
      this.$router.push({ path: "/" });
    },
  },
};
</script>

<style >
body {
  @apply bg-orange-400;
  background-color: orange;
}
* {
  font-family: "Roboto Mono";
}
a {
  display: block;
}
</style>


<style scoped>
.wrapper-word {
  box-shadow: 10px 10px 1px black;
  height: 10vh;
}
</style>