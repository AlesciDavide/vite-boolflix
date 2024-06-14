<script>
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
            this.store.searchFilm = this.inputSearch;
            this.inputSearch = '',
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
        },
    }
}
</script>

<template>
    <input type="text" placeholder="Cerca un film" v-model="inputSearch" @keyup.enter="getFilms">
    <button @click="getFilms">Cerca</button>
</template>

<style scoped>

</style>