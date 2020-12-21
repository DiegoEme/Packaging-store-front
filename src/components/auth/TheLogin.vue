<template>
  <v-layout>
    <v-container   >

    <v-row class="d-flex justify-center"
    >
      <v-col cols="6">
        <v-card class="pa-5"
        >
          <v-form 
          
          ref="form" 
          lazy-validation>
            <v-text-field
              v-model="login.email"
              label="Email"
              required
            ></v-text-field>

            <v-text-field
              v-model="login.password"
              label="Password"
              type="password"
              required
            ></v-text-field>

            <v-btn
              :disabled="!(this.login.email && this.login.password)"
              color="info"
              class="mr-4"
              block
              @click="loginUser"
            >
              Login
            </v-btn>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
    </v-container>

  </v-layout>
</template>

<script>
import swal from "sweetalert";
import axios from 'axios'
export default {
  name: "TheLogin",
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  beforeCreate(){
    this.$store.dispatch('autoLogin') ? this.$router.push({path: '/segura'}) : false;
  },
  methods: {
    loginUser() {
      axios.post('http://localhost:3000/api/usuario/login', this.login)
        .then(response => {
           return response.data;
          })
        .then(data => {
          this.$store.dispatch('guardarToken', data.tokenReturn)
          this.$router.push({name: 'Segura'});
          swal("Exito!", "Login correcto!", "success");
          console.log(data);
        })
        .catch(error => {
          swal("Oops!", "Algo salió mal!", "error");
          console.log(error);
          return error;
        })
    },
  }  
};
</script>

<style scoped></style>
