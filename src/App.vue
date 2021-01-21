<template>
  <v-app>
    <Navbar />
    <v-main>
      <router-view></router-view>
    </v-main>
    <Footers />
  </v-app>
</template>

<script>
import Navbar from "../src/components/NavBar";
import Footers from "../src/components/Footer";

export default {
  name: "App",

  components: {
    Navbar,
    Footers
  },

  data: () => ({
    //
  })
};
</script>
