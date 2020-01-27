<template>
  <v-container>
    <v-app-bar
        :collapse="!collapseOnScroll"
        :collapse-on-scroll="collapseOnScroll"
        fixed
        color="teal accent-4"
        dark
        shrink-on-scroll
        scroll-threshold="300"
        src="https://ahmadmahmoud.sirv.com/portfolio/images/navbar-bg1.jpg"
        fade-img-on-scroll
      >
        <template v-slot:img="{ props }">
          <v-img
            v-bind="props"
            gradient="to top right, rgba(55,236,186,.7), rgba(25,32,72,.7)"
          ></v-img>
        </template>
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

        <v-toolbar-title>
            <h1 class="title">Ahmad Mahmoud</h1>
            <h2 class="subtitle-1"><v-icon left>fas fa-briefcase</v-icon> Web Developer</h2>
        </v-toolbar-title>
        

        <v-spacer></v-spacer>
        <v-avatar tile>
          <img
            src="https://ahmadmahmoud.sirv.com/portfolio/images/me.png?w=100&h=100&thumbnail=100"
            alt="Ahmad"
          >
        </v-avatar>
        
    </v-app-bar>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      temporary
      id="navDrawer"
    >
      <v-list-item dark class="teal accent-4">
        <v-list-item-avatar tile>
          <v-img src="https://ahmadmahmoud.sirv.com/portfolio/images/me.png?w=100&h=100&thumbnail=100"></v-img>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title>Ahmad Mahmoud</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense>

        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :href="item.link"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-container>

</template>

<script>
  export default {
    data: () => ({
      collapseOnScroll: true,
      drawer: false,
      items: [],
    }),
    created() {
      const contentful = require("contentful");
      const client = contentful.createClient({
        // This is the space ID. A space is like a project folder in Contentful terms
        space: "5iqet69iikf0",
        // This is the access token for this space. Normally you get both ID and the token in the Contentful web app
        accessToken: "q4pra6Sk2s7sfAJqYNtODWBktPe8Jl1_pSpX1JRfQFk"
      });
      // This API call will request an entry with the specified ID from the space defined at the top, using a space-specific access token.
      client.getEntries()
      .then((response) => {
        response.items.forEach(item => {
          this.items.push({
            title: item.fields.title,
            icon: item.fields.icon,
            link: '#' + item.fields.title,
            id: item.sys.id
          })
        })
      })
    }
    
  }
</script>

<style scoped>
#navDrawer {
  background-color: #FFFDF1;
}
</style>