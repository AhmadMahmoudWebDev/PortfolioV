<template>
  <v-footer
    dark
    padless
  >
    <v-card
      class="flex"
      flat
      tile
    >
      <v-card-text class="teal accent-4 text-center">
        <strong class="title">Please Contact Me on social networks!</strong>

        <v-spacer></v-spacer>

        <v-btn
          v-for="social in socials"
          :key="social.name"
          class="mx-4"
          dark
          icon
          :href="social.link"
          target="_blank"
          ripple
        >
          <v-icon size="24px">{{ social.icon }}</v-icon>
        </v-btn>
      </v-card-text>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>Ahmad Mahmoud</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
  export default {
    data: () => ({
      socials: [
          {
            name: 'gmail',
            link: 'mailto:ahmadmahmoud.webdev@gmail.com',
            icon: 'fab fa-google'
          },
          {
            name: 'facbook',
            link: 'https://www.facebook.com/ahmadmahmoud.webdev',
            icon: 'fab fa-facebook'
          },
          {
            name: 'github',
            link: 'https://github.com/AhmadMahmoudWebDev',
            icon: 'fab fa-github'
          },
          {
            name: 'linkedin',
            link: 'https://www.linkedin.com/in/ahmad-mahmoud-159499191',
            icon: 'fab fa-linkedin'
          }
      ],
    }),
  }
</script>