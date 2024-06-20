<template>
    <div class="flex flex-col ">
        <SavedMovies :movies="savedMovies" />
        <button @click="sendImage">Buscar Sales</button>
        <div class=" grid md:grid-cols-4 lg:grid-cols-6 xl:grid-cols-12 grid-cols-2 gap-6">
            <div @click="saveMovie(item.imdbID)"
                class=" w-36 flex flex-col flex-wrap shadow-lg rounded-md bg-emerald-600" v-for="item in movies"
                :key="item.imdbID">
                <div class=" w-36 h-56"><img class=" h-full w-full object-cover" v-bind:src="item.Poster" alt="">
                </div>
                <div class=" h-[120px] m-1">
                    <p>{{ item.Title }}</p>
                    <p>{{ item.Year }}</p>
                </div>
                <div v-show="showDetails">
                    <p>Hola</p>
                </div>
                <button class=" " @click="showDetails = !showDetails">Details</button>

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
    watch:{
        
    },

    methods: {
        saveMovie(id) {
            let savedMovie = this.movies.find(item => item.imdbID == id)
            this.savedMovies.push(savedMovie)
            console.log(this.savedMovies);



            // for (item in this.movies){
            //     if(item.imbID==id){
            //         this.savedMovie=item
            //         this.savedMovies.push(this.savedMovie)
            // }}
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





    }

}
</script>
<style></style>