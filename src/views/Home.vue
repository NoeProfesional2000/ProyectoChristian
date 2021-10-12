<template>
  <!-- App.vue -->
  <v-app>
    <v-app-bar app color="#ff8000">
      <v-app-bar-nav-icon
        @click.stop="drawer = !drawer"
        color="#ffffff"
      ></v-app-bar-nav-icon>
      <div>
        <h2 style="color: white">Sistema</h2>
      </div>
      <v-spacer></v-spacer>
      <v-btn icon color="#ffffff">
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-btn icon color="#ffffff">
        <v-icon>mdi-filter</v-icon>
      </v-btn>
      <v-btn icon color="#ffffff">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <Navigation :drawer="drawer"></Navigation>

    <!-- Sizes your content based upon application components -->
    <Body></Body>

    <Footer></Footer>
  </v-app>
</template>

<script>
import Footer from "./Footer.vue";
import Body from "./Body.vue";
import Navigation from "./Navigation.vue";

export default {
  data: () => ({
    drawer: false,
  }),
  components: {
    Footer,
    Body,
    Navigation,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
