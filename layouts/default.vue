<template>
  <v-app>
    <v-navigation-drawer
      v-model="isDrawerOpen"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-tile
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title" />
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar :clipped-left="clipped" fixed app>
      <v-toolbar-side-icon @click="isDrawerOpen = !isDrawerOpen" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>{{ `chevron_${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-chip v-if="!isProd" color="warning">
        <span class="hidden-md-and-down">This is a&nbsp;</span>
        test
        <span class="hidden-xs-only">&nbsp;environment</span>
        <span class="hidden-md-and-down"
          >, things will break, data will be deleted</span
        >!
      </v-chip>
    </v-toolbar>
    <v-content>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer absolute inset app height="120" class="py-12">
      <v-layout justify-center wrap>
        <v-flex py-3 text-xs-center xs12
          >This project is supported by funding from the Australian Government
          Department of Agriculture, Water and the Environment as part of its
          Rural R&amp;D for Profit program.</v-flex
        >
        <div class="logo">
          <v-img src="/Agrifutures-Securing.png" width="200px"></v-img>
        </div>
        <div class="logo">
          <v-img src="/dawelogo.png" width="200px"></v-img>
        </div>
      </v-layout>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: true,
      isDrawerOpen: false,
      fixed: true,
      miniVariant: false,
      title: 'Pollin8',
    }
  },
  computed: {
    isProd() {
      return this.$store.state.isProd
    },
    items() {
      const result = [
        {
          icon: 'home',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-folder',
          title: 'Project overview and media',
          to: '/project',
        },
        {
          icon: 'memory',
          title: 'Run simulation',
          to: '/simulation',
        },
        {
          icon: 'school',
          title: 'About the science',
          to: '/science',
        },
        {
          icon: 'mdi-tree-outline',
          title: 'Revegetation Planting Guide',
          to: '/planting',
        },
        {
          icon: 'mdi-bee-flower',
          title: 'Native Bee Food Calendar',
          to: '/flowering',
        },
      ]
      return result
    },
  },
  mounted() {
    const isViewportWideEnough = window.innerWidth > 1263
    if (isViewportWideEnough) {
      this.isDrawerOpen = true
    }
  },
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

.logo {
  padding: 10px 10px 1px 10px;
}
</style>
