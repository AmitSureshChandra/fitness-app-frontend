<template>
  <v-card>
    <v-card-title>
      Members
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :loading="loading"
      :items="data"
      :search="search"
    ></v-data-table>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  name: "HomePage",
  mounted() {
    axios
      .get("/api/admin/users")
      .then(({ data }) => {
        this.data = data.data;
        this.loading = true;
      })
      .catch((e) => {
        console.log({ e });
      })
      .finally(() => {
        this.loading = false;
      });
  },
  data: () => {
    return {
      search: "",
      loading: false,
      headers: [
        {
          text: "User ID",
          align: "start",
          sortable: false,
          value: "id",
        },
        { text: "role", value: "role_id" },
        { text: "name", value: "name" },
        { text: "email", value: "email" },
      ],
      data: [],
    };
  },
};
</script>

<style>
</style>