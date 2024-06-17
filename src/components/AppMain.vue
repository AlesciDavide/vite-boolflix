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

        <h1 v-if="store.films.length > 0">Films</h1>
        <section class="container-film">
            <ul>
                <li v-for="film in store.films">
                    
                    <img class="my-img-not-found" v-if="film.poster_path == null"  src="..//assets/img/no-image.jpg" alt="Image not found">
                    <img v-else :src="'https://image.tmdb.org/t/p/w342/' + film.poster_path" alt="">

                    <div class="my-hover">
                        <p>
                            {{film.title}}
                        </p>
                        <img v-if="(film.original_language.toUpperCase() == 'JA')" :src="'https://flagsapi.com/JP/flat/32.png'">
                        <img v-else-if="(film.original_language.toUpperCase() == 'EN')" :src="'https://flagsapi.com/GB/flat/32.png'">
                        <img v-else :src="'https://flagsapi.com/' + film.original_language.toUpperCase() + '/flat/32.png'">
                        {{film.original_title }}<br>
                        {{film.original_language}}<br>
                        {{film.vote_average}}
                        <i v-for="star in (Math.floor(film.vote_average / 2))" class="fa-solid fa-star"></i>
                        <i v-for="star in (5 - Math.floor(film.vote_average / 2))" class="fa-regular fa-star"></i>

                    </div>
                </li>
            </ul>
        </section>
        <h1 v-if="store.series.length > 0">Series</h1>
        <section class="container-series">
            <ul>
                <li v-for="serie in store.series">
                    <img class="my-img-not-found" v-if="serie.poster_path == null"  src="..//assets/img/no-image.jpg" alt="Image not found">
                    <img v-else :src="'https://image.tmdb.org/t/p/w342/' + serie.poster_path" alt="">

                    <div class="my-hover">
                        {{serie.original_name}} <br>

                        <img v-if="(serie.original_language.toUpperCase() == 'JA')" :src="'https://flagsapi.com/JP/flat/32.png'">
                        <img v-else-if="(serie.original_language.toUpperCase() == 'EN')" :src="'https://flagsapi.com/GB/flat/32.png'">
                        <img v-else-if="(serie.original_language.toUpperCase() == 'HI')" alt="HI">
                        <img v-else :src="'https://flagsapi.com/' + serie.original_language.toUpperCase() + '/flat/32.png'">
                        {{serie.original_title }}<br>
                        {{serie.vote_average}}
                        <i v-for="star in (Math.floor(serie.vote_average / 2))" class="fa-solid fa-star"></i>
                        <i v-for="star in (5 - Math.floor(serie.vote_average / 2))" class="fa-regular fa-star"></i>

                    </div>
                </li>
            </ul>
        </section>
</template>

<style lang="scss" scoped>
    
    h1{
        color: white;
        width: 98vw;
        margin: 0 auto;
        
    }
    img{
        object-fit: cover;
        height: 100%;
    }
    .container-film{
        overflow-x: scroll;
        width: 98vw;
        margin: 0 auto;
        
            ul{
                display: flex;
                flex-direction: row;
                    li{
                        display: flex;
                        flex-direction: column;
                        position: relative;
                        padding: .3rem;
                        &:hover{
                            opacity: .5;
                            transition: all 0.25s ease-out;
                                .my-hover{
                                    display: inline;
                            }
            }
                    }
            }
            
    }
    .container-series{
        display: flex;
        overflow-x: scroll;
        width: 98vw;
        margin: 0 auto;
            ul{
                display: flex;
                justify-content: center;
                flex-direction: row;
                li{
                        display: flex;
                        flex-direction: column;
                        position: relative;
                        padding: .3rem;
                        &:hover{
                            opacity: .5;
                                .my-hover{
                                    display: inline;
                            }
            }
                    }
            }
    }

    .my-img-not-found{
        width: 342px;
    }

    .my-hover{
        display: none;
        position: absolute;

    }


</style>