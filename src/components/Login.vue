<template>
  <div>
    <v-card class="mx-auto" max-width="344">
      <v-toolbar dark color="primary">
        <v-toolbar-title>Login form </v-toolbar-title>
      </v-toolbar>
      <v-card-text>
         <v-text-field
          v-model="user.email"
          :rules="[rules.required, rules.email]"
          label="E-mail"
        ></v-text-field>
        <v-text-field
          v-model="user.password"
          :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required, rules.min]"
          :type="show ? 'text' : 'password'"
          name="input-10-1"
          label="Password"
          hint="At least 8 characters"
          counter
          @click:append="show = !show"
        ></v-text-field>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          text
          dark
          color="primary"
          v-on:click="loginSubmit()"
          v-on:keyup="loginSubmit()"
        >
          Login
        </v-btn>
      </v-card-actions>
    </v-card>
    <div>
      <v-snackbar v-model="snackbar" :timeout="snckbar_timeout">
        {{ text }}
        <template v-slot:action="{ attrs }">
          <v-btn color="pink" text v-bind="attrs" @click="snackbar = false">
           
          </v-btn>
        </template>
      </v-snackbar>
      
    </div>
  </div>
  
</template>

<script>
import axios from "axios";
export default {
  name: "Login",

  data() {
    return {
      user: {
        password: "",
        email: "",
      },
      key: "",
      show: false,
      snackbar: false,
      text: "",
      snckbar_timeout: 2000,
      rules: {
        required: (value) => !!value || "Required",
        min: (v) => v.length >= 8 || "Min 8 characters",
        emailMatch: () => `The email and password you entered don't match`,
        email: (value) => {
          const pattern =
            /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return pattern.test(value) || "Invalid e-mail.";
        },
      },
    };
  },
  methods: {
    async loginSubmit() {
      await axios
        .post(
          `https://v2202107122785158474.goodsrv.de/api/rest-auth/login/`,
          this.user
        )
        .then((response) => {
          console.log(response);
          if (response.status == 200) {
             this.snackbar = true;
           this.text = `You have loged in sucssfully`;
            let key = response.data.key;
            axios
              .get(
                "https://v2202107122785158474.goodsrv.de/api/rest-auth/user/",
                {
                  headers: { Authorization: `Token ${key}` },
                }
              )
              .then((response) => {
                this.$emit("userData", response.data);
                this.$emit("show", true);
              });
          }
        })
        .catch((error) => {
          console.log(error);
          this.text = `Error`;
          this.snackbar = true;
        });
    },
  },
};
</script>
<style scoped>
</style>

