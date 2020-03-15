<template>
  <div id="app">
    <v-app id="inspire">
      <app-nav />
      <router-view class="page" />
    </v-app>
  </div>
</template>
<script>
import AppNav from './components/AppNav'
export default {
  components: { AppNav }
}
</script>

//
<style lang="scss">
// @import './assets/styles/global.scss';
// .page {
//   display: flex;
//   justify-content: center;
//   flex-direction: column;
//   align-items: center;
//   min-height: calc(100vh - 56px);
// }
//
</style>

//
<!-- 
// <script>
// import HelloWorld from './components/HelloWorld'

// export default {
//   name: 'App',

//   components: {
//     HelloWorld
//   },

//   data: () => ({
//     //
//   })
// }
// </script> -->
