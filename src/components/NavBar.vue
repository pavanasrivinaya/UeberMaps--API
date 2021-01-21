<template>
  <div>
    <v-app-bar app color="primary" dark>
      <router-link to="/"><h1 class="heading">Uebermaps</h1></router-link>
      <v-spacer></v-spacer>
      <v-btn router to="/" text rounded class="mr-3">Home</v-btn>
      <v-btn router to="/about" text rounded>About</v-btn>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: "navbar"
};
</script>
<style scoped>
a {
  text-decoration: none;
}
.heading {
  color: white;
}
</style>
