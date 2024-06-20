<template>
  <div class=" flex flex-col">
    <h1 class=" text-emerald-500">
      Find your favourite Movies

    </h1>
    <form @submit.prevent="getInfo">
      <input type="text" v-model="movieTitle">
      <button type="submit">Enviar</button>
    </form>

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

      fetch(`http://www.omdbapi.com/?apikey=${this.aKey}&s=${this.movieTitle}`)
        .then(response => response.json())
        .then(response => {
          this.movies = response.Search;

        }
        )
        .catch(err => console.error(err));
      this.movieTitle = ""

    },
    getImage(obj) {
      this.image = obj
    }

  },


}
</script>
<style></style>