<script>
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';
import {store} from './store.js';

export default{
    components:{
      AppMain,
      AppHeader,
    },
      data() {
          return{
              
          }
      }
}
</script>

<template>
  <AppHeader/>
  <main>

    <AppMain/>
  </main>
</template>

<style lang="scss">
@use './styles/general.scss' as *;
main{
        background-color: #191919;
        height: calc(100vh - 48.43px);
        overflow: auto;
    }
</style>