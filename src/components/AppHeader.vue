<script>
import MainSearch from '../components/MainSearch.vue'
import {store} from '../store.js';
export default{
    components:{
        MainSearch,
        store,
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
    }
}
</script>

<template>
    <section>
        <div>
            <img src="../assets/img/logo.png" alt="Netflix">
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
        </div>
    </section>
</template>

<style scoped>
    section{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: .5rem 0;
        background-color: #191919;
            div{
                display: flex;
                justify-content: center;
                flex-direction: row;
                color: white;
            }
    }
    ul{
        display: flex;
        flex-direction: row;
        align-items: center;
    }
    img{
        width: 120px;
    }
</style>