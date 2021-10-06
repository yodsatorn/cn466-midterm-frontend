<template>
  <v-card>
    <v-card-title>
      Incubator
      <v-spacer></v-spacer>

      <v-select
        v-model="select"
        :items="select_items"
        style="max-width: 300px;"
        class="mx-3"
      ></v-select>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
        style="max-width: 300px;"
        class="mt-n4"
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
  data() {
    return {
      // Data table
      data: [],
      search: "",

      // Select box
      select: 1,
      select_items: [
        { text: "Incubator #1", value: 1 },
        { text: "Incubator #2", value: 2 },
        { text: "Incubator #3", value: 3 },
        { text: "ALL", value: -1 },
      ],

      // UI function
      loading: true,
    };
  },
  computed: {
    headers() {
      return [
        {
          text: "Incubator",
          value: "IncubatorID",
          filter: (value) => {
            if (this.select == -1 || value == this.select) {
              return true;
            }
            return false;
          },
        },
        { text: "pressure", value: "pressure" },
        { text: "temperature", value: "temperature" },
        { text: "humidity", value: "humidity" },
        { text: "timestamp", value: "timestamp" },
      ];
    },
  },
  methods: {},
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

<style></style>
