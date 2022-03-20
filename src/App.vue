<template>
  <div id="app">
    <v-app>
      <v-main>
        <login-page v-if="!auth" @loggedIn="setAuth()" />
        <div v-else>
          <v-app-bar
            ><v-app-bar-nav-icon
              @click.stop="drawer = !drawer"
            ></v-app-bar-nav-icon>
            <v-app-bar-title style="font-size: 20px">
              Fitness Admin Panel</v-app-bar-title
            >
            <v-spacer />
            <v-btn
              :disabled="loading"
              right
              text
              class="primary float-right"
              @click="logout()"
            >
              Logout
              <v-progress-circular
                class="ml-1"
                v-if="loading == true"
                indeterminate
                :width="3"
                size="20"
                color="white"
              ></v-progress-circular>
            </v-btn>
          </v-app-bar>
          <v-navigation-drawer v-model="drawer" absolute temporary>
            <v-list-item>
              <v-list-item-avatar>
                <v-img
                  src="data:image/png;base64,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"
                ></v-img>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>{{
                  this.user && this.user.name ? this.user.name : "Admin"
                }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list dense>
              <v-list-item
                selectable
                v-for="(item, index) in items"
                :key="item.title"
                link
                @click="
                  {
                    value = index;
                    drawer = false;
                  }
                "
                :class="index === value ? 'primary white--text' : ''"
              >
                <v-list-item-icon>
                  <v-icon :color="index === value ? 'white' : ''">{{
                    item.icon
                  }}</v-icon>
                </v-list-item-icon>

                <v-list-item-content>
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-navigation-drawer>
          <v-container>
            <template v-if="value == 0">
              <home-page />
            </template>

            <template v-if="value == 1">
              <daily-attendence />
            </template>

            <template v-if="value == 2">
              <gym-data />
            </template>

            <template v-if="value == 3">
              <user-membership />
            </template>

            <template v-else> </template>
          </v-container>
          <!-- <v-bottom-navigation :value="value" color="teal" grow>
          <v-btn>
            <span>Recents</span>

            <v-icon>mdi-history</v-icon>
          </v-btn>

          <v-btn>
            <span>Favorites</span>

            <v-icon>mdi-heart</v-icon>
          </v-btn>

          <v-btn>
            <span>Nearby</span>

            <v-icon>mdi-map-marker</v-icon>
          </v-btn>
        </v-bottom-navigation> -->
        </div>
      </v-main>
    </v-app>
  </div>
</template>

<script>
import DailyAttendence from "./components/DailyAttendence.vue";
import UserMembership from "./components/UserMembership.vue";
import GymData from "./components/GymData.vue";
import HomePage from "./components/HomePage.vue";
import LoginPage from "./components/LoginPage.vue";
import axios from "axios";
export default {
  name: "App",
  components: { DailyAttendence, GymData, UserMembership, HomePage, LoginPage },
  data() {
    return {
      auth: false,
      email: "",
      password: "",
      loading: false,
      user: {
        email: "",
        name: "",
      },
      value: 1,
      drawer: false,
      items: [
        { title: "Home", icon: "mdi-view-dashboard" },
        { title: "Attendence", icon: "mdi-calendar-plus" },
        { title: "Gym Data", icon: "mdi-clipboard-text" },
        { title: "Membership", icon: "mdi-wallet-membership" },
      ],
    };
  },
  mounted() {
    let isLoggedIn = JSON.parse(localStorage.getItem("loggedIn"));
    if (isLoggedIn && isLoggedIn == true) {
      axios.defaults.headers.Authorization = JSON.parse(
        localStorage.getItem("access_token")
      );
      this.user = JSON.parse(localStorage.getItem("user"));
      this.auth = true;
    }
  },
  methods: {
    setAuth() {
      this.auth = true;
      this.user = JSON.parse(localStorage.getItem("user"));
    },
    logout() {
      this.loading = true;
      axios
        .post("/api/logout", {
          email: this.email,
          password: this.password,
        })
        .then(({ status }) => {
          if (status == 200) {
            localStorage.clear();
            this.auth = false;
          }
        })
        .catch((e) => {
          console.log({ e });
        })
        .finally(() => {
          this.loading = false;
        });
    },
  },
};
</script>

<style>
.v-app-bar-title__content {
  width: 125px;
}
</style>
