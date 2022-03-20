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
    this.loading = true;

    axios
      .get("/api/admin/users")
      .then(({ data }) => {
        this.data = data.data;
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
          value: "user_id",
        },
        { text: "Role", value: "user_role" },
        { text: "Name", value: "user_name" },
        { text: "Email", value: "user_email" },
      ],
      data: [],
    };
  },
};
</script>

<style>
</style>