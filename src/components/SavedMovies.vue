<template>
    <div class=" grid md:grid-cols-4 lg:grid-cols-6 xl:grid-cols-8 grid-cols-3 gap-6">
        <div class=" items-center  md:w-36 w-28 flex flex-col flex-wrap shadow-lg rounded-md bg-red-500" v-for="item in movies"
            :key="item.imdbID">
            <div class=" md:w-36 md:h-56 w-28 h-36 relative">
                <img class=" h-full w-full object-cover rounded-t-md" v-bind:src="item.Poster" alt="">
                <button @click="emitDeleteMovie(item.imdbID)"
                    class=" hover:bg-red-400 absolute top-0 font-mono font-semibold rounded-full md:text-base text-sm right-0 px-1.5 md:px-2 bg-red-500 ">x</button>
            </div>
            <div class=" md:text-base text-sm md:h-[120px] h-24 w-28 md:m-1">
                <p>{{ item.Title }}</p>
                <p>{{ item.Year }}</p>

            </div>
            <div v-show="info">
                <p>Hola</p>
            </div>
            <button class=" md:w-[130px] w-[80px] md:text-base text-sm mb-2" @click="selectCard(item.imdbID)">Details</button>

        </div>
    </div>
</template>
<script>

export default {
    name: "SavedMovies",
    components: {},
    props: ["movies"],
    data() {
        return {
            savedMovies: this.movies,
            info:false
        }
    },
    methods: {
        emitDeleteMovie(id) {

            return this.$emit('delete', id)
        },
        selectCard(id){
            console.log(id)

        
            
        }
    },

}


</script>
<style></style>