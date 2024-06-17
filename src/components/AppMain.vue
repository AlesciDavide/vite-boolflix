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
                        <p>
                            {{film.title}}
                        </p>
                        
                        <img  v-if="film.original_language == 'en'" class="flag" src="https://flagcdn.com/16x12/gb.png">
                        <img class="flag" v-else-if="film.original_language == 'it'" src="https://flagcdn.com/16x12/it.png" alt="">

                        <p v-if="film.title != film.original_title">
                            {{film.original_title }}

                        </p>
                        <p>

                            {{Math.floor(film.vote_average / 2)}}
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
                        <p>
                            {{serie.original_name}} 

                        </p>

                        
                        <img  v-if="serie.original_language == 'en'" class="flag" src="https://flagcdn.com/16x12/gb.png">
                        <img class="flag" v-else-if="serie.original_language == 'it'" src="https://flagcdn.com/16x12/it.png" alt="">
                        <p v-if="serie.original_name != serie.original_title">
                            {{serie.original_title }}

                        </p>
                        <p>

                            {{Math.floor(serie.vote_average / 2)}}
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
    
    h1{
        color: white;
        width: 98vw;
        margin: 0 auto;
        
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
                            transition: all 0.25s ease-out;
                                .my-hover{
                                    display: flex;
                                    flex-direction: column;
                                    
                                    
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
        aspect-ratio: 1/1;
        
    }
.flag{
    width: 30px;
    height: 20px;
}

</style>