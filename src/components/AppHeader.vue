<script>
import MainSearch from '../components/MainSearch.vue';
import {store} from '../store.js';

export default{
    components:{
        MainSearch,
    },
    data() {
        return{
            headerLinks:[
                {
                    id: 1,
                    name: 'Home',
                    active: true,
                },
                {
                    id: 2,
                    name: 'Serie Tv',
                    active: false,
                },
                {
                    id: 3,
                    name: 'Film',
                    active: false,
                },
                {
                    id: 4,
                    name: 'Originali',
                    active: false,
                },
                {
                    id: 5,
                    name: 'Aggiunto di recente',
                    active: false,
                },
                {
                    id: 6,
                    name: 'La mia lista',
                    active: false,
                },
            ],
            store,
            
        }
    },
}
</script>

<template>
    <header>

        <section>
            <div>
                <img src="../assets/img/Boolflix.svg" alt="Boolflix">
                <ul>
                    <li v-for="link in headerLinks">
                        {{link.name}}
                    </li>
                </ul>
            </div>
            <div>
                        <MainSearch/>
                        <h2>Bambini</h2>
                        <i class="fa-regular fa-bell"></i>
                        <img class="my_users" src="../assets/img/ui.png" alt="">
                        <i class="fa-solid fa-caret-down"></i>
            </div>
        </section>
    </header>
</template>

<style lang="scss" scoped>
header{
    background-color: #191919;
}
    section{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: .5rem 0;
        width: 98vw;
        margin: 0 auto;
            div{
                display: flex;
                justify-content: center;
                flex-direction: row;
                color: white;
                align-items: center;
            }
    }
    ul{
        display: flex;
        flex-direction: row;
        align-items: center;
            li{
                margin-right: 1rem;
                font-size: 1.2rem;
            }
    }
    img{
        width: 110px;
        margin-right: .5rem;
    }
    .my_users{
        height: 30px;
        width: 30px;
        margin-left: 1.5rem;
    }
    
    h2{
        margin-right: .5rem;
    }
</style>