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
            flag: [],
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
                        <h2>
                            {{film.title}}
                        </h2>
                        <img class="flag lang-icon" :class="'lang-icon-' + film.original_language" src="" alt="">
                        <p v-if="film.title != film.original_title">
                            {{film.original_title }}
                        </p>
                        <p class="overview">
                            {{ film.overview }}
                        </p>
                        <div>
                            <i v-for="star in (Math.floor(film.vote_average / 2))" class="fa-solid fa-star"></i>
                            <i v-for="star in (5 - Math.floor(film.vote_average / 2))" class="fa-regular fa-star"></i>
                        </div>
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
                        <h2>
                            {{serie.original_name}} 

                        </h2>

                        <img class="flag lang-icon" :class="'lang-icon-' + serie.original_language" src="" alt="">
                        <p v-if="serie.original_name != serie.original_title">
                            {{serie.original_title }}
                        </p>
                        <p>
                            {{ serie.overview }}
                        </p>
                        <div>
                            <i v-for="star in (Math.floor(serie.vote_average / 2))" class="fa-solid fa-star"></i>
                            <i v-for="star in (5 - Math.floor(serie.vote_average / 2))" class="fa-regular fa-star"></i>
                        </div>

                    </div>
                </li>
            </ul>
        </section>
</template>

<style lang="scss" scoped>
@use '../styles/partials/flags' as *;
    
    h1{
        color: white;
        width: 98vw;
        margin: 0 auto;
        
    }
    h2{
        font-size: 2rem;
        color: white;
    }
    .fa-solid{
        color: yellow;
    }
    img{
        object-fit: cover;
        height: 100%;
    }
    .container-film,
    .container-series{
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
                        color: white;
                        font-size: 1.5rem;
                        &:hover{
                            
                                .my-hover{
                                    display: flex;
                                    flex-direction: column;
                                    align-items: center;
                                    justify-content: end;
                                    padding: 2rem 0;

                                    
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
        background-color:rgb(0, 0, 0, 0.5);
        height: 100%;
        width: -moz-available;
        
    }
.overview{
    height: 150px;
    overflow: auto;
    margin-left: .3rem;
    padding: 0 .3rem;
}

.lang-icon{
                    background-image: url(../assets/img/lang-flags.png);
                }
</style>