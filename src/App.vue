<template>
  <div id="app">
    <v-app>
      <v-main>
        <v-app-bar
          ><v-app-bar-nav-icon
            @click.stop="drawer = !drawer"
          ></v-app-bar-nav-icon>
          <v-app-bar-title style="font-size: 20px">
            Fitness App</v-app-bar-title
          >
        </v-app-bar>
        <v-navigation-drawer v-model="drawer" absolute temporary>
          <v-list-item>
            <v-list-item-avatar>
              <v-img
                src="https://avatars.githubusercontent.com/u/47358181?v=4"
              ></v-img>
            </v-list-item-avatar>

            <v-list-item-content>
              <v-list-item-title>Amit Kesarwani</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

          <v-divider></v-divider>

          <v-list dense>
            <v-list-item v-for="item in items" :key="item.title" link>
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>

              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-navigation-drawer>
        <v-container> All pages go here </v-container>
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
      </v-main>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      email: "akumar00029@gmail.com",
      password: "password",
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
  mounted() {},
};
</script>

<style>
.v-app-bar-title__content {
  width: 125px;
}
</style>
