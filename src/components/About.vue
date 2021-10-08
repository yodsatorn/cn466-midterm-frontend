<template>
  <v-container>
    <h1>About page</h1>
    <v-card class="mx-auto" max-width="800">
      <v-img
        src="https://images.pexels.com/photos/3183190/pexels-photo-3183190.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940"
        height="300px"
      ></v-img>
      <v-card-title>
        CN466 - Midterm Project
      </v-card-title>
      <v-card-subtitle>
        This project is about ....
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
          <v-card-text>
            Member <br />
            - 6110613095 : Yodsatorn Pantongkam <br />
            - 6110613129 : Rathapol Putharaksa <br />
            - 6110613228 : Poonnatuch Boonyarattanasoontorn <br />
          </v-card-text>
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
