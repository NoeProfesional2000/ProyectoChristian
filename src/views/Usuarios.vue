

<template>
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

    <v-main>
      <v-container fluid>
        <v-card>
          <v-card-title>
            <v-btn color="primary" dark class="mb-2">
              Nuevo Usuario
            </v-btn>
            <v-spacer></v-spacer>
            <v-text-field label="Buscar" v-model="search"></v-text-field>
          </v-card-title>
          <v-data-table
            :headers="headers"
            :items="datos_usuarios"
            :items-per-page="5"
            class="elevation-1"
            :search="search"
            :custom-filter="filterOnlyCapsText"
          >
          </v-data-table>

          <router-view></router-view>
        </v-card>
      </v-container>
    </v-main>

    <Footer></Footer>
  </v-app>
</template>

<script>
import Footer from "./Footer.vue";
import Navigation from "./Navigation.vue";

export default {
  data() {
    return {
      search: '',
      drawer: false,
      headers: [
        { text: "ID", value: "id" },
        { text: "USER ID", value: "userId" },
        { text: "TITLE", value: "title" },
        { text: "COMPLETE", value: "completed" },
      ],
      datos_usuarios: [],
    };
  },
  components: {
    Footer,
    Navigation,
  },
  mounted() {
    //Constructor lo que vaya aqui se inicializa primero...
    this.getDatos();
  },
  methods: {
    getDatos: async function() {
      const axios = require("axios");
      axios.defaults.baseURL = "https://jsonplaceholder.typicode.com";
        
        axios.get("/todos")
        .then((Response) => {
          this.datos_usuarios = Response.data;
        })
        .catch((Response) => {
          console.log(Response);
        });
    },
    filterOnlyCapsText (value, search) {
        return value != null &&
          search != null &&
          typeof value === 'string' &&
          value.toString().toLocaleLowerCase().indexOf(search) !== -1
      },
  },
};
</script>