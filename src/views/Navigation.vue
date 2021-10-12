<template>
  <v-navigation-drawer app v-model="drawer" absolute bottom temporary>
    <v-list nav dense>
      <v-list-item-group
        v-model="group"
        active-class="deep-orange--text text--accent-4"
      >
        <v-list-item :href="'/'">
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Home</v-list-item-title>
        </v-list-item>

        <v-list-item :href="'/usuarios'">
          <v-list-item-icon>
            <v-icon>mdi-widgets</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Usuarios</v-list-item-title>
        </v-list-item>

        <v-list-item>
          <v-list-item-icon>
            <v-icon>mdi-message</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Fizz</v-list-item-title>
        </v-list-item>

        <v-list-item @click="generarReporte()">
          <v-list-item-icon>
            <v-icon>mdi-chat</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Reporte</v-list-item-title>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-navigation-drawer>
</template>
<script>
import { jsPDF } from "jspdf";

export default {
  props: {
    drawer: Boolean,
  },
  data: () => ({
    group: null,
  }),
  methods: {
    generarReporte(){
      // Default export is a4 paper, portrait, using millimeters for units
      const doc = new jsPDF();

      doc.text("EJEMPLO DE REPORTE EN DASHBOARD", 10, 10);
      doc.save("Reporte.pdf");
    }
  },
  watch: {
    group() {
      this.drawer = false;
    },
  },
};
</script>
