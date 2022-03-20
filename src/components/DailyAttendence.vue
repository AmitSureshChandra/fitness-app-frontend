<template>
  <v-card>
    <v-card-title>
      Attendence Data
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
      :items="data"
      :loading="loading"
      :search="search"
    ></v-data-table>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  name: "DailyAttendence",
  mounted() {
    axios
      .get("/api/admin/attendences")
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
          value: "user_id",
        },
        { text: "Branch ID", value: "branch_id" },
        { text: "Date", value: "date" },
        { text: "Time", value: "time" },
        { text: "Action", value: "action" },
        { text: "CreatedAt", value: "created_at" },
      ],
      data: [],
    };
  },
};
</script>

<style>
</style>