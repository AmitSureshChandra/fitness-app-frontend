<template>
  <v-card>
    <v-card-title>
      Body Data
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
  name: "GymData",
  mounted() {
    this.loading = true;

    axios
      .get("/api/admin/data")
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
          text: "User",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "date", value: "date" },
        { text: "neck", value: "neck" },
        { text: "shoulder", value: "shoulder" },
        { text: "chest", value: "chest" },
        { text: "arms", value: "arms" },
        { text: "forearms", value: "forearms" },
        { text: "thighs", value: "thighs" },
        { text: "calf", value: "calf" },
        { text: "weight", value: "weight" },
      ],
      data: [],
    };
  },
};
</script>

<style>
</style>