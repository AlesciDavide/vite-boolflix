<script>
import axios from 'axios';
import {store} from '../store.js';
export default{
    data() {
        return{
            store,
            inputSearch: '',
        }
    },
    methods:{
        getFilms(){
            if (this.inputSearch.length > 0) {
                this.store.searchFilm = this.inputSearch;
                axios.get('https:/api.themoviedb.org/3/search/movie?api_key=1231079dd3a1fe954db3fe98b67aa52f&language=it-IT&query=' + store.searchFilm).then(response => {
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
                
            };
            if (this.inputSearch.length > 0) {
                this.store.searchFilm = this.inputSearch;
                this.inputSearch = '',
                axios.get('https://api.themoviedb.org/3/search/tv?api_key=1231079dd3a1fe954db3fe98b67aa52f&language=it_IT&query=' + store.searchFilm).then(response => {
                    this.store.series = response.data.results;
                    console.log(response.data.results);
                    
                })
                .catch(function (error) {
                    // handle error
                    console.log(error);
                })
                .finally(function () {
                    // always executed
                });
                
            };

        },
    }
}
</script>

<template>
    <input type="text" placeholder="Cerca un film" v-model="inputSearch" @keyup.enter="getFilms">
    <button @click="getFilms"><i class="fa fa-search"></i></button>
</template>

<style lang="scss" scoped>
    input {
        max-width: 40px;
        transition: all 0.25s ease-out;
        margin-right: .5rem;
    }
    input:focus {
        max-width: 180px;
    }
    button{
        color: white;
        background-color: transparent;
        border: none;
        margin-right: .5rem;
    }

</style>