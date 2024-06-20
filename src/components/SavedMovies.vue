<template>
    <div class="flex gap-6">
        <div  class=" flex flex-col flex-wrap w-36 shadow-lg rounded-md bg-red-500"
        v-for="item in movies" :key="item.Title">
        <img v-bind:src="item.Poster" alt="">
        <p>{{ item.Title }}</p>
        <p>{{ item.Year }}</p>
        <div v-show="showDetails">
            <p>Hola</p>
        </div>
        <button @click="showDetails = !showDetails">Details</button>

    </div>
    </div>
</template>
<script>

export default {
    name:"SavedMovies",
    components:{},
    props:["movies"],
    data(){
        return{

        }
    },
    methods:{

    }
    
}
</script>
<style>
    
</style>