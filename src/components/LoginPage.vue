<template>
  <div id="app">
    <v-app>
      <v-main>
        <v-layout align-center>
          <v-container style="width: 250px">
            <v-row justify="center">
              <v-card width="400" height="250">
                <v-card-title class="text-center"> Fitness App </v-card-title>

                <v-card-text>
                  <v-row>
                    <v-col class="my-0" cols="12">
                      <v-text-field
                        type="email"
                        label="Email"
                        dense
                        v-model="email"
                      />
                    </v-col>

                    <v-col class="my-0" cols="12">
                      <v-text-field
                        v-model="password"
                        :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                        :rules="[rules.required]"
                        :type="show1 ? 'text' : 'password'"
                        name="input-10-1"
                        label="Password"
                        counter
                        dense
                        @click:append="show1 = !show1"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-card-text>
                <v-card-actions class="float-right">
                  <v-btn
                    @click="login()"
                    :disabled="loading"
                    depressed
                    color="primary"
                  >
                    Login

                    <v-progress-circular
                      class="ml-1"
                      v-if="loading == true"
                      indeterminate
                      :width="3"
                      size="20"
                      color="white"
                    ></v-progress-circular>
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-row>
          </v-container>
        </v-layout>
      </v-main>
    </v-app>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "LoginPage",
  data() {
    return {
      show1: false,
      show2: true,
      email: "admin@gmail.com",
      loading: false,
      password: "password",
      rules: {
        required: (value) => !!value || "Required.",
        min: (v) => v.length >= 8 || "Min 8 characters",
        emailMatch: () => `The email and password you entered don't match`,
      },
    };
  },

  methods: {
    login() {
      axios.get("/sanctum/csrf-cookie").then(() => {
        this.loading = true;
        axios
          .post("/api/login?type=admin", {
            email: this.email,
            password: this.password,
          })
          .then(({ data, status }) => {
            if (status === 200) {
              localStorage.setItem("loggedIn", JSON.stringify(true));
              localStorage.setItem(
                "access_token",
                JSON.stringify("Bearer " + data.token)
              );
              axios.defaults.headers.Authorization = "Bearer " + data.token;
              localStorage.setItem("user", JSON.stringify(data.user));

              this.$swal(
                `Welcome ${data.user.name}! `,
                "Login Successful",
                "success"
              ).then(() => {
                this.$emit("loggedIn");
              });
            }
          })
          .catch((e) => {
            console.log({ e });
          })
          .finally(() => {
            this.loading = false;
          });
      });
    },
  },
};
</script>

<style>
</style>
