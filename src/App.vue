<template>
  <v-app>
    <v-main class="background">
      <Header/>
      <searchBox/>
      <gidSearchBox/>
    </v-main>
  </v-app>
</template>

<script>
import gidSearchBox from './components/gidSearchBox.vue';
import Header from './components/HelloWorld';
import searchBox from './components/searchBox';

export default {
  name: 'App',

  components: {
    Header,
    searchBox,
    gidSearchBox,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
.background{
  background: black;
  opacity: 0.8;
  background-image: url('../src/assets/background.png');
  background-attachment: fixed;
}

</style>
