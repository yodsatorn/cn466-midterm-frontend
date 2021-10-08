<template>
  <v-card>
    <v-card-title>
      Incubator
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
        style="max-width: 300px;"
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="data"
      :loading="loading"
      :search="search"
    >
    </v-data-table>
  </v-card>
</template>

<script>
import axios from "axios";

export default {
  props: {
    select: Number,
  },

  data() {
    return {
      // Data table
      data: [],
      search: "",

      // UI function
      loading: true,
    };
  },
  computed: {
    headers() {
      return [
        { text: "temperature", value: "temperature" },
        { text: "humidity", value: "humidity" },
        { text: "pressure", value: "pressure" },
        { text: "timestamp", value: "timestamp" },
        { text: "Incubator", value: "IncubatorID" },
      ];
    },
  },
  methods: {
  },
  beforeCreate() {
    axios
      .get("https://cn466-mid-server.herokuapp.com/Incubator/All")
      .then((response) => {
        this.data = response.data.data;
      })
      .catch((err) => {
        console.log(err);
      })
      .finally(() => {
        this.loading = false;
      });
  },
};
</script>

<style>
tbody tr:nth-of-type(odd) {
  background-color: rgba(41, 151, 255, 0.5);
}
</style>
