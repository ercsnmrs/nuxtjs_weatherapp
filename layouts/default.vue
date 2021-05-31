<template>
  <v-app>
    <v-card
      color="lighten-4"
      flat
      tile
    >
      <v-toolbar dense>
        <v-app-bar-nav-icon />

        <v-toolbar-title>
          <nuxt-link
            to="/weather-app"
            class="brown darken-4"
          >
            Weather App
          </nuxt-link>
        </v-toolbar-title>

        <v-spacer />
      </v-toolbar>
    </v-card>

    <v-main>
      <nuxt />
    </v-main>

    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>
<style scoped>
a{
  text-decoration: none;
  color:white;
}
</style>
