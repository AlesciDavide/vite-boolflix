<script>
import axios from 'axios';
import {store} from '../store.js';
import MainSearch from '../components/MainSearch.vue'
export default{
    components:{
        MainSearch,

    },
    data() {
        return{
            store,
        }
    },
    methods:{
        getFilmsStart(){
            
            axios.get('https://api.themoviedb.org/3/trending/movie/day?api_key=1231079dd3a1fe954db3fe98b67aa52f&language=it-IT').then(response => {
                
                this.store.films = response.data.results;
                console.log(response.data.results);
                
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        },
    },
    created(){
        this.getFilmsStart();
        
        
    },
}
</script>

<template>
    <ul>
        <li v-for="film in store.films">
            {{film.title}} <br>
                <img v-if="film.poster_path.length > 0" :src="'https://image.tmdb.org/t/p/w342/' + film.poster_path" alt="">
                <img v-else src="" alt="Image not found"> <br>
            <img v-if="(film.original_language.toUpperCase() == 'JA')" :src="'https://flagsapi.com/JP/flat/32.png'">
            <img v-else-if="(film.original_language.toUpperCase() == 'EN')" :src="'https://flagsapi.com/GB/flat/32.png'">
            <img v-else-if="(film.original_language.toUpperCase() == 'HI')" alt="HI">
            <img v-else :src="'https://flagsapi.com/' + film.original_language.toUpperCase() + '/flat/32.png'">
            {{film.original_title }}<br>
            {{film.original_language}}<br>
            {{film.vote_average}}
        </li>
        <li v-for="film in store.series">
                <img v-if="film.poster_path.length > 0" :src="'https://image.tmdb.org/t/p/w342/' + film.poster_path" alt="">
                <img v-else src="" alt="Image not found">
            {{film.original_name}} <br>
            <img v-if="(film.original_language.toUpperCase() == 'JA')" :src="'https://flagsapi.com/JP/flat/32.png'">
            <img v-else-if="(film.original_language.toUpperCase() == 'EN')" :src="'https://flagsapi.com/GB/flat/32.png'">
            <img v-else-if="(film.original_language.toUpperCase() == 'HI')" alt="HI">
            <img v-else :src="'https://flagsapi.com/' + film.original_language.toUpperCase() + '/flat/32.png'">
            {{film.original_title }}<br>
            {{film.vote_average}}

        </li>
    </ul>
</template>

<style scoped>

</style>