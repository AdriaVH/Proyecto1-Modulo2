<template>
    <div class="flex flex-col items-center ">
        <SavedMovies @delete="deleteSavedMovie" :movies="savedMovies" />
        <button class=" m-8 w-36 h-12" @click="sendImage">Mostrar Sala</button>
        <div class="grid md:grid-cols-4 lg:grid-cols-6 xl:grid-cols-8 grid-cols-3 gap-6">
            <div @click="saveMovie(item.imdbID)"
                class=" items-center hover:shadow-emerald-500 hover:shadow-2xl md:w-36 w-28 flex flex-col flex-wrap shadow-lg rounded-md bg-emerald-600"
                v-for="item in movies" :key="item.imdbID">
                <div class=" md:w-36 md:h-56 w-28 h-36"><img class=" h-full w-full object-cover rounded-t-md"
                        v-bind:src="item.Poster" alt="">
                </div>
                <div class=" md:text-base text-sm md:h-[120px] h-24 w-28 md:m-1">
                    <p>{{ item.Title }}</p>
                    <p>{{ item.Year }}</p>
                </div>
                <div v-show="showDetails">
                    <p>Hola</p>
                </div>
                <button class=" md:w-[130px] w-[80px] md:text-base text-sm mb-2"
                    @click="showDetails = !showDetails">Details</button>

            </div>
        </div>
    </div>

</template>
<script>
import SavedMovies from "./SavedMovies.vue"



export default {
    name: "ShowMovies",
    props: ["movies"],
    components: { SavedMovies },
    data() {
        return {
            showDetails: false,
            // id: undefined,
            // savedMovie:{},
            savedMovies: [],
            image: {},
        }
    },
    mounted() {
        this.fetchImage()

    },
    watch: {

    },

    methods: {
        saveMovie(id) {
            let savedMovie = this.movies.find(item => item.imdbID == id)

            let predicate = (e) => e.imdbID == id
            if (!this.savedMovies.some(predicate)) {
                this.savedMovies.push(savedMovie)
            }

        },
        fetchImage() {
            fetch("https://api.unsplash.com/photos/woman-sitting-on-red-folding-armchair-jLRIsfkWRGo/?client_id=1sRIHf2T8a--OhtqfKLMWJnFxusN-0zzqBsfNhCFeuY")
                .then(response => response.json())
                .then(data => {
                    this.image = data
                })
                .catch(error => console.log(error))
        },
        sendImage() {
            this.$emit('image', this.image)
        },
        deleteSavedMovie(id) {
            this.savedMovies = this.savedMovies.reduce((acc, movie) => {
                if (movie.imdbID !== id) {
                    acc.push(movie);
                }
                return acc;
            }, []);
            return this.savedMovies
        }





    }

}
</script>
<style></style>