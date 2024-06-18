<script>
import {store} from '../store.js';
export default{
    data() {
        return{
            store,
        }
    }
}
</script>

<template>

    <h1 v-if="store.films.length > 0">Films</h1>
        <h1 v-else>Films not found</h1>
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

</template>

<style lang="scss" scoped>
@use '../../node_modules/@textabledev/langs-flags-list/lang-flags.css' as *;

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
    .container-film{
        overflow-x: scroll;
        overflow-y: clip;
        width: 98vw;
        margin: 0 auto;
        margin-bottom: 3rem;
        
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
                        border: 3px solid rgb(92, 92, 92);
                        box-shadow: 2px white;
                        &:hover{

                            .my-hover{
                                    display: flex;
                                    flex-direction: column;
                                    align-items: center;
                                    justify-content: end;
                                    padding: 2rem 0;
                                    background-color:rgb(0, 0, 0, 0.8);
                                    animation: gigi .5s linear;
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
        height: 100%;
        width: -moz-available;
        bottom: 0;
        left: 0;
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

@keyframes gigi {
    0%{
        height: 0%;
        background-color:rgb(0, 0, 0, 0.1);
    }
    25%{
        height: 25%;
        background-color:rgb(0, 0, 0, 0.3);
    }
    50%{
        height: 50%;
        background-color:rgb(0, 0, 0, 0.5);
    }
    75%{
        height: 75%;
        background-color:rgb(0, 0, 0, 0.6);
    }
    100%{
        height: 100%;
        background-color:rgb(0, 0, 0, 0.8);
    }
    
}
</style>