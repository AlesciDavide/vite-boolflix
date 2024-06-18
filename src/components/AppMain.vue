<script>
import axios from 'axios';
import {store} from '../store.js';
import MainSearch from '../components/MainSearch.vue'
import MainFilm from '../components/MainFilm.vue'
import MainSeries from '../components/MainSeries.vue';
export default{
    components:{
        MainSearch,
        MainFilm,
        MainSeries

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
    
    <MainFilm/>
    <MainSeries/>
        
</template>

<style lang="scss" scoped>


</style>