<template>
  <!-- Sizes your content based upon application components -->
  <v-main>
    <!-- Provides the application the proper gutter -->
    <v-container fluid>
      <div class="text-center">
        <h1
          style="
            padding-bottom: 40px;
            padding-top: 30px;
          "
        >
          WELCOME!!
        </h1>
      </div>
      <div class="row">
        <div class="col-sm">
          <v-card>
            <v-card-title>GRÁFICA DE PASTEL</v-card-title>
            <chartjs-doughnut v-bind:labels="labels" v-bind:datasets="datasets" v-bind:option="option"></chartjs-doughnut>
          </v-card>
        </div>
        <div class="col-sm">
          <v-card>
            <v-card-title>GRÁFICA DE BARRAS</v-card-title>
            <chartjs-bar v-bind:labels="labels_1" v-bind:datasets="datasets_1" v-bind:option="option"></chartjs-bar>  
          </v-card>
        </div>
      </div>
    </v-container>
  </v-main>
</template>

<script >
export default {
  data(){
    return {
      labels: ['Completados', 'Aun por terminar'],
      labels_1: ['User 1', 'User 2', 'User 3', 'User 4','User 5', 'User 6', 'User 7', 'User 8', 'User 9','User 10'],
      datasets:[
        {
          data: [90,110],
          backgroundColor:[
            "Red",
            "Yellow"
          ]
        }
      ],
      datasets_1:[
        {
          data: [20,20,20,20,20,20,20,20,20,20,20],
          backgroundColor:[
            "Red",
            "Yellow",
            "Purple",
            "Orange",
            "Gray",
           "Blue",
           "Green",
           "Brown",
            "Red",
            "Yellow",
          ]
        }
      ],
      datos_usuarios:[],
      valores: [],
      verdadero: 0,
      falso: 0,
      option: {
        title:{
          display:true,
          position: "bottom",
          text: "Custom chart"
        }
      }
    }
  },
  mounted(){
    this.getCompletes();
  },
  methods:{
    getCompletes() {
      const axios = require("axios");
      axios.defaults.baseURL = "https://jsonplaceholder.typicode.com";
        
        axios.get("/todos")
        .then((Response) => {
          this.datos_usuarios = Response.data;
          for(var i = 0; i < this.datos_usuarios.length; i++){
            if(this.datos_usuarios[i]['completed'] === false){
              this.verdadero++;
            }else{
              this.falso++;
            }
          }
          console.log(this.verdadero);
          this.data[0] = this.verdadero;
          this.data[1] = this.falso;
        })
        .catch((Response) => {
          console.log(Response);
        });
    }
  }
}
</script>