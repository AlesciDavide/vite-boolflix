<script>
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';
import {store} from './store.js';

export default{
    components:{
      AppMain,
      AppHeader,
      store,
    },
      data() {
          return{
              
          }
      }
}
</script>

<template>
  <AppHeader/>
  <AppMain/>

</template>

<style lang="scss">
@use './styles/general.scss' as *;

</style>