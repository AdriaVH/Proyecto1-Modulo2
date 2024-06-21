<template>
  <div class=" flex flex-col items-center">
    <div
      class=" justify-center justify-around h-64 w-80 md:h-80 md:w-[700px] mb-10 flex flex-col md:gap-4 gap-6 shadow-emerald-500 shadow-2xl rounded-3xl">
      <h1 class=" md:text-6xl text-emerald-500">
        Find your favourite <br> 🎞️ Movies 🎞️
      </h1>
      <form class="flex flex-col items-center gap-8 h-28 md:h-30" @submit.prevent="getInfo">
        <input
          class=" h-6 md:h-10 md:w-96 w-60 rounded-lg  text-emerald-500 border-transparent focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-transparent"
          type="text" placeholder="Lord of the Rings" v-model="searchTitle">
        <button
          class=" md:text-lg text-base md:w-28 md:h-14 w-20 h-10 text-emerald-500 hover:bg-emerald-500 hover:text-emerald-950"
          type="submit">Buscar</button>
      </form>
    </div>

    <ShowMovies @image="getImage" :movies="movies" v-if="movies" />
    <img v-bind:src="image.urls.full" alt="" v-if="image">



  </div>
</template>
<script>
//imports
import ShowMovies from "./components/ShowMovies.vue"
export default {
  name: "App",
  components: { ShowMovies },

  data() {
    return {
      movieTitle: "",
      aKey: "2ac0417",
      movies: [],
      image: null

    }
  },
  methods: {
    getInfo() {
      if (this.searchTitle !== "") {
        fetch(`http://www.omdbapi.com/?apikey=${this.aKey}&s=${this.searchTitle}`)
          .then(response => response.json())
          .then(response => {
            this.movies = response.Search;

          }
          )
          .catch(err => console.error(err));
        this.searchTitle = ""
      }

    },
    getImage(obj) {
      this.image = obj
    }

  },


}
</script>
<style></style>