<template>
  <v-container>
    <h1>About us</h1>
    <v-card class="mx-auto" style="max-width:100% ;">
      <v-img
        src="https://images.pexels.com/photos/3183190/pexels-photo-3183190.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940"
        height="400px"
      ></v-img>
      <v-card-title class="text-h5">
        CN466 - Midterm Project
      </v-card-title>
      <v-card-subtitle class="text-body-1">
        This project is built as part of the CN466 midterm project, the front-end is provided by Yodsatorn Pantongkam using Vue.js as the framework front-end for development. 
      </v-card-subtitle>
      <v-card-actions>
        <v-btn color="orange lighten-2" text>
          Explore
        </v-btn>
        <v-spacer></v-spacer>
        <v-btn icon @click="show = !show">
          <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
        </v-btn>
      </v-card-actions>
      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>
          <v-card-title>
            Member
          </v-card-title>
          <v-card-subtitle>
            - 6110613095 : Yodsatorn Pantongkam <br />
            - 6110613129 : Rathapol Putharaksa <br />
            - 6110613228 : Poonnatuch Boonyarattanasoontorn <br />
          </v-card-subtitle>
          <v-col>
            <v-icon large>
              mdi-github
            </v-icon>
            <v-text> Back-end APIs : </v-text>
            <a href="https://www.instagram.com/poonnatuchh/"
              >Link to Git repository</a
            >
            <br />
            <br />
            <v-icon large>
              mdi-github
            </v-icon>
            <v-text> Front-end : </v-text>
            <a href="https://github.com/yodsatorn/cn466-midterm-frontend.git"
              >Link to Git repository</a
            >
            <br />
            <br />
            <v-icon large>
              mdi-github
            </v-icon>
            <v-text> Line Chatbot : </v-text>
            <a href="https://github.com/Rathapol-Putharaksa/linebot_CN466"
              >Link to Git repository</a
            >
          </v-col>
        </div>
      </v-expand-transition>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    show: false,
  }),
};
</script>

<style></style>
