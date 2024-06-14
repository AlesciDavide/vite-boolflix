<script>
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';
import AppCreatedFlag from './components/AppCreatedFlag.vue';
import {store} from './store.js';

export default{
    components:{
      AppMain,
      AppHeader,
      AppCreatedFlag,
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
<AppCreatedFlag/>
</template>

<style lang="scss">
@use './styles/general.scss' as *;

</style>