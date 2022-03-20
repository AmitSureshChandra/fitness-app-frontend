<template>
  <v-card>
    <v-card-title>
      Membership Data
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
  name: "UserMembership",
  mounted() {
    this.loading = true;

    axios
      .get("/api/admin/memberships")
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
        { text: "Payment Mode", value: "payment_mode" },
        { text: "amount", value: "amount" },
        { text: "months", value: "months" },
        { text: "status", value: "status" },
        { text: "Created At", value: "created_at" },
      ],
      data: [],
    };
  },
};
</script>

<style>
</style>