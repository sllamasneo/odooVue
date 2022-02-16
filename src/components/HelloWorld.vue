<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3 ma-10"
          contain
          height="200"
        />
        <!-- <router-link to="/about" class="mb-10 pb-10">Link a la página de about</router-link> -->
        <v-form v-model="valid">
          <v-container>
            <v-row class="d-flex justify-center">
              <v-col cols="6">
                <v-row>
                  <v-text-field
                    v-model="firstname"
                    :counter="10"
                    label="First name"
                    required
                  ></v-text-field>
                </v-row>

                <v-row>
                  <v-col cols="12" md="6"
                    ><v-btn elevation="2" @click="ejemplo"
                      >Enviar datos a odoo</v-btn
                    ></v-col
                  >
                </v-row>
                <v-row>
                  <h1>Datos directamente de odoo</h1>
                  <table class="default">
                    <tr>
                      <th>Id</th>

                      <th>Nombre</th>

                      <th>Plazas</th>
                    </tr>

                    <tr v-for="(item, index) in data" :key="index">
                      <td>{{ item.id }}</td>
                      <td>{{ item.name }}</td>
                      <td>{{ item.plazas }}</td>
                    </tr>
                  </table>
                </v-row>
              </v-col>
            </v-row>
          </v-container>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  created() {
    axios.get(`http://localhost:8080/consulta`).then((value) => {
      this.data = value.data;
    });
  },
  data: () => ({
    valid: false,
    firstname: "",
    data: "",
  }),
  methods: {
    ejemplo() {
      axios
        .post(`http://localhost:8080/webpage?nombre=${this.firstname}`)
        .then(() => {
          axios.get(`http://localhost:8080/consulta`).then((value) => {
            this.data = value.data;
            console.log(this.data);
          });
        })
        .then(alert("Datos enviados correctamente"));
    },
  },
};
</script>
