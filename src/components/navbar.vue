<template>
  <div>
    <v-toolbar color="white">
        <router-link to="/">
          <img class="NavLogo" src="../img/logo/vehicle_rent_logo.png">
        </router-link>
      <v-spacer class></v-spacer>
      <v-toolbar-side-icon class="hidden-md-and-up" @click="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <v-navigation-drawer app v-model="drawer" class disable-resize-watcher>
      <v-list>
        <template v-for="(item, index) in items">
          <v-list-tile :key="index">
            <v-list-tile-content>{{item.title}}</v-list-tile-content>
          </v-list-tile>
          <v-divider :key="`divider-${index}`"></v-divider>
        </template>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  name: 'AppNavigation',
  data () {
    return {
      drawer: false,
      dropdown_font: ['test', 'testsa', 'sgfdsfdas', 'gsdfasf'],
      dropdown_font1: ['test', 'testsa', 'sgfdsfdas', 'gsdfasf'],
      items: [
        { title: 'Valuta' },
        { title: 'Jezik' }
      ]
    }
  },
  computed: {
    isAuthenticated () {
      return this.$store.getters.isAuthenticated
    }
  },
  methods: {
    logout () {
      this.$store.dispatch('userSignOut')
    }
  }
}
</script>

<style scoped>
a {
  color: white;
  text-decoration: none;
}
.NavLogo {
  max-width: 150px;
}
</style>
