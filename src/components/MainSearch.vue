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
    background-color: #383838;
    border: 1ex solid none;
    border-top-width: 1.7em;
    margin: 0;
    padding: 0;
    color: #383838;
    word-wrap: break-word;
    outline: 7px solid #383838;
    height: 30px;
    font-size: 17px;
    text-align: center;
    transition: all .5s;
    max-width: 190px;
    font-weight: bold;
    font-family: 'Courier New', Courier, monospace;
    }

    input:hover {
    border-top-width: 0.2em;
    background-color: #f1e8e8;
    }

    input:focus {
    border-top-width: 0.2em;
    background-color: #f1e8e8;
    
    }
    button{
            background-color: #383838;
        border: 1ex solid none;
        border-top-width: 1.7em;
        margin: 0;
        padding: 0;
        color: #383838;
        word-wrap: break-word;
        outline: 7px solid #383838;
        height: 30px;
        font-size: 17px;
        text-align: center;
        transition: all .5s;
        max-width: 190px;
        font-weight: bold;
        font-family: 'Courier New', Courier, monospace;
        display: flex;
        align-items: self-end;
        margin-right: 1rem;
            i{
                font-size: x-large;
            }
        }

</style>