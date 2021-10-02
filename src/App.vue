<template>
  <v-app id="app">
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md4>
          <div role="alert" v-if="logged == false">
            <Login v-on:userData="onclickdata" v-on:show="onclickshow" />
          </div>
          <div role="alert" v-if="logged == true">
            <v-card class="elevation-16 mx-auto" width="300">
              <v-card-title class="text-h5">
                <p>hello {{ username }}</p>
              </v-card-title>
              <v-card-text>
                <p>ID : {{ pk }}</p>
                <p>Email : {{ email }}</p>
                <p>Staff : {{ is_staff }}</p>
              </v-card-text>
             
              <div class="text-center mt-12">
                 <v-divider></v-divider>
                  <v-rating
                    v-model="rating"
                    color="yellow darken-3"
                    background-color="grey darken-1"
                    empty-icon="$ratingFull"
                    half-increments
                    hover
                    x-small
                  ></v-rating>
                </div>
            </v-card>
          </div>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
import Login from "./components/Login.vue";
export default {
  name: "App",
  components: {
    Login,
  },
  data() {
    return {
      logged: false,
      show: true,
      username: "",
      email: "",
      pk: 0,
      is_staff: true,
      rating: 4.5,
    };
  },
  methods: {
    onclickdata(value) {
      this.username = value.username;
      this.email = value.email;
      this.pk = value.pk;
      this.is_staff = value.is_staff;
    },

    onclickshow(value) {
      this.logged = value;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
