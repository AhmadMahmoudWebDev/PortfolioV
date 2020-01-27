<template>
  <v-app>
    <Navbar />
      <v-content>
        <v-container>
            <Nuxt />
        </v-container>
      </v-content>
      <Footer />
  </v-app>
</template>

<script>
import Navbar from './NavBar'
import Footer from './Footer'

export default {
  name: 'App',

  components: {
    Navbar,
    Footer,
  },

  data: () => ({
    //
  }),
};
</script>

<style scoped>
#app {
  background-color: #FFFDF1;
  background-image: url('https://ahmadmahmoud.sirv.com/portfolio/images/portfolio%20bg.png');
  background-position: center;
  background-size: contain;
}
</style>
