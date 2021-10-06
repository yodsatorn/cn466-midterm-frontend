<template>
  <v-app>
    <ul>
      <li>
        <router-link to="/"> Home </router-link>
      </li>
      <li>
        <router-link to="/about"> About </router-link>
      </li>
    </ul>

    <router-view></router-view>
  </v-app>
</template>

<script>
export default {};
</script>

<style scoped>
ul li {
  display: inline;
}
ul li {
  margin-right: 5px;
}
</style>
