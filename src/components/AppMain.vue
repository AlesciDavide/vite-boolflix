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
            inputSearch: '',
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
            {{film.original_title }}<br>
            {{film.original_language}}<br>
            {{film.vote_average}}
        </li>
    </ul>
</template>

<style scoped>

</style>