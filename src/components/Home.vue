<template>
  <v-container>
    <h1>
      Home
    </h1>
    <v-spacer></v-spacer>
    <v-card class="mx-auto" style="max-width:100% ;">
      <v-card-title>
        Incubator status
        <v-spacer></v-spacer>
        <v-select
          v-model="select"
          :items="select_items"
          style="max-width: 300px;"
          class="mx-3"
        ></v-select>
      </v-card-title>
      <v-container fluid>
        <v-row>
          <v-col v-for="card in cards" :key="card.title" :cols="card.flex">
            <v-card :loading="loading">
              <v-img
                :src="card.src"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title v-text="card.title"></v-card-title>
              </v-img>
              <v-card-subtitle>
                {{ card.text }} 
              </v-card-subtitle>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <br>
      <v-card-title>Temperature</v-card-title>
      <v-sparkline
        :value="getTempInID(this.select)"
        :gradient="gradientTemp"
        :smooth="radius || false"
        :padding="padding"
        :line-width="width"
        :stroke-linecap="lineCap"
        :gradient-direction="gradientDirection"
        :fill="fill"
        :type="type"
        :auto-line-width="autoLineWidth"
        auto-draw
      ></v-sparkline>
      <br>
      <v-card-title>Humidity</v-card-title>
      <v-sparkline
        :value="getHumidInID(this.select)"
        :gradient="gradientHumid"
        :smooth="radius || false"
        :padding="padding"
        :line-width="width"
        :stroke-linecap="lineCap"
        :gradient-direction="gradientDirection"
        :fill="fill"
        :type="type"
        :auto-line-width="autoLineWidth"
        auto-draw
      ></v-sparkline>
      <br>
      <v-card-title>Pressure</v-card-title>
      <v-sparkline
        :value="getPressInID(this.select)"
        :gradient="gradientPress"
        :smooth="radius || false"
        :padding="padding"
        :line-width="width"
        :stroke-linecap="lineCap"
        :gradient-direction="gradientDirection"
        :fill="fill"
        :type="type"
        :auto-line-width="autoLineWidth"
        auto-draw
      ></v-sparkline>
      <incubatortable :select="select"></incubatortable>
    </v-card>
  </v-container>
</template>

<script>
import axios from "axios";
import IncubatorTable from "./IncubatorTable.vue";

const gradients = [
  
  ["#2980B9", "#6DD5FA", "#FFEDBC", "#ED4264" ],
  ["#5433FF", "#20BDFF", "#A5FECB"],
  ["#4AC29A",  "#BDFFF3"],
  
];

export default {
  components: {
    incubatortable: IncubatorTable,
  },
  data: () => ({

    //unit
    tempUnit: "   °C",
    humidUnit: "   %",
    pressUnit: "   PA",

    //array for chart
    temp1: [],
    temp2: [],
    temp3: [],
    humid1: [],
    humid2: [],
    humid3: [],
    press1: [],
    press2: [],
    press3: [],

    // Select box
    select: 1,
    select_items: [
      { text: "Incubator #1", value: 1 },
      { text: "Incubator #2", value: 2 },
      { text: "Incubator #3", value: 3 },
    ],

    // UI function
    loading: true,
    cards: [
      {
        title: "Temperature  ( °C )",
        src:
          "https://images.pexels.com/photos/1454752/pexels-photo-1454752.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940",
        flex: 4,
        text: "",
      },
      {
        title: "Humidity  ( % )",
        src:
          "https://images.pexels.com/photos/2929290/pexels-photo-2929290.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940",
        flex: 4,
        text: "",
      },
      {
        title: "Pressure  ( Pa )",
        src:
          "https://media.istockphoto.com/photos/pressure-device-for-industry-system-picture-id908299346?k=20&m=908299346&s=612x612&w=0&h=iWFvONEvcXN7sxh6t0J4E8lsT61y3jBbpCGZf2fqnGs=",
        flex: 4,
        text: "",
      },
    ],
    width: 1,
    radius: 10,
    padding: 8,
    lineCap: "round",
    gradientTemp: gradients[0],
    gradientHumid: gradients[1],
    gradientPress: gradients[2],
    gradientDirection: "top",
    gradients,
    fill: false,
    type: "trend",
    autoLineWidth: false,
  }),
  methods: {
    getInfo(InID) {
      axios
        .get(`https://cn466-mid-server.herokuapp.com/Incubator/Latest/${InID}`)
        .then((response) => {
          this.cards[0].text = (response.data.data.temperature);
          this.cards[1].text = (response.data.data.humidity);
          this.cards[2].text = (response.data.data.pressure);
        })
        .catch((err) => {
          console.log(err);
        })
        .finally(() => {
          this.loading = false;
        });
    },
    getTempInID(InID) {
      if (InID == 1) {
        return this.temp1;
      } else if (InID == 2) {
        return this.temp2;
      } else {
        return this.temp3;
      }
    },
    getHumidInID(InID) {
      if (InID == 1) {
        return this.humid1;
      } else if (InID == 2) {
        return this.humid2;
      } else {
        return this.humid3;
      }
    },
    getPressInID(InID) {
      if (InID == 1) {
        return this.press1;
      } else if (InID == 2) {
        return this.press2;
      } else {
        return this.press3;
      }
    },
    tempFormatted(rawTemp){
      var formattedTemp;
      formattedTemp = rawTemp+" °C";
      return formattedTemp;
    },
    humidFormatted(rawHumid){
      var formattedHumid;
      formattedHumid = rawHumid+" %";
      return formattedHumid;
    },
    pressFormatted(rawPress){
      var formattedPress;
      formattedPress = rawPress+" Pa"
      return formattedPress
    },
  },
  beforeCreate() {
    axios
      .get(`https://cn466-mid-server.herokuapp.com/Incubator/All`)
      .then((response) => {
        let data = response.data.data;
        data.forEach((element) => {
          if (element.IncubatorID == 1) {
            this.temp1.push(parseFloat(element.temperature));
            this.humid1.push(parseFloat(element.humidity));
            this.press1.push(parseFloat(element.pressure));
          } else if (element.IncubatorID == 2) {
            this.temp2.push(parseFloat(element.temperature));
            this.humid2.push(parseFloat(element.humidity));
            this.press2.push(parseFloat(element.pressure));
          } else if (element.IncubatorID == 3) {
            this.temp3.push(parseFloat(element.temperature));
            this.humid3.push(parseFloat(element.humidity));
            this.press3.push(parseFloat(element.pressure));
          }
        });
      })
      .catch((err) => {
        console.log(err);
      });
  },
  created() {
    setInterval(() => {
      this.getInfo(this.select);
    }, 15000);
  },
};
</script>

<style></style>
