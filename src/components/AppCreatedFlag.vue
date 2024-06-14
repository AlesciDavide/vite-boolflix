<script>
import {store} from '../store.js';
import axios from 'axios';
export default{
    data() {
        return{
            flag: [],
            store,
        }
    },
    methods:{
        searchFlag(){
            
            axios.get('https://restcountries.com/v3.1/all').then(response => {
                console.log(response.data);
                this.flag = response.data;
                
                for (let i = 0; i < this.flag.length; i++) {
                    let singleFlag = {
                    countrie: this.flag[i].cca2,
                    flag: this.flag[i].flags.png,
                } 
                    store.flag.push(singleFlag);
                }
                console.log(store.flag)
                
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
        this.searchFlag();
        
        
    },
}
</script>

<template>

</template>

<style scoped>

</style>