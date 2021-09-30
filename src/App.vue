<template>
  <v-app id="app">
    <v-container fluid fill-height>
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md4>
             <div role="alert" v-if="logged == false">
                <Login v-on:userData="onclickdata" v-on:show="onclickshow"/>
             </div>
              <div role="alert" v-if="logged == true">
              <p>ID : {{ pk }}</p>
               <p>hello {{ username }}</p>
               <p>Email :  {{ email }}</p>
               <p>Staff : {{  is_staff }}</p>
              
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
    };
  },
  methods: {
    onclickdata (value) {
      this.username = value.username
      this.email = value.email
      this.pk = value.pk
      this.is_staff = value.is_staff
    },

    onclickshow (value) {
      this.logged = value
    }
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
