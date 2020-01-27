<template>
  <v-timeline align-top :dense="$vuetify.breakpoint.smAndDown">
    <v-timeline-item
      v-for="(item, i) in items"
      :key="i"
      :color="item.color"
      :icon="item.icon"
      fill-dot
    >
      <v-lazy
        v-model="item.isActive"
        :options="{
          threshold: 0.5,
        }"
        min-height="200"
        transition="fade-transition"
      >
        <v-card
          :color="item.color"
          dark
          :id="item.title"
        >
          <v-card-title class="title"><h3>{{ item.title }}</h3></v-card-title>
          <v-img 
            :src="item.src"
            :lazy-src="item.lazySrc"
          >
            <template v-slot:placeholder>
              <v-row
                class="fill-height ma-0"
                align="center"
                justify="center"
              >
                <v-progress-circular indeterminate color="teal accent-4"></v-progress-circular>
              </v-row>
            </template>
          </v-img>
          <v-card-text class="white text--primary">
            <p>{{ item.description }}</p>
            <v-btn
              :color="item.color"
              class="mx-0"
              :href="item.visit"
              target="_blank"
              outlined
              block
            >
              <v-icon left>fa-link</v-icon> Visit The site
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn
              :color="item.color"
              class="mx-0"
              :href="item.github"
              target="_blank"
              outlined
              block
            >
              <v-icon left>fab fa-github</v-icon> View Git Source
            </v-btn>
          </v-card-text>
          <v-spacer></v-spacer>
          <v-card-actions>
            <h4 class="card-text"><v-icon left>fas fa-box</v-icon> Stack Used</h4>
            <v-spacer></v-spacer>
            <v-btn
              icon
              @click="item.showInfo = !item.showInfo"
            >
              <v-icon>{{ item.showInfo ? 'fa-chevron-up' : 'fa-chevron-down' }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="item.showInfo">
              <v-divider></v-divider>
              <v-list-item v-for="(stack, s) in item.stackUsedJson" :key="s">
                <v-list-item-content>
                  <v-list-item-title>{{ stack }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </div>
          </v-expand-transition>
        </v-card>
      </v-lazy>
    </v-timeline-item>
  </v-timeline>
</template>

<script>


  export default {
    data: () => ({
      items: []
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
            ...item.fields,
            id: item.sys.id
          })
        })
      })
    }
  }
</script>

<style scoped>
    .v-timeline {
        margin-top: 5rem;
    }
    .laravel-color {
      color: #F05340;
    }
</style>