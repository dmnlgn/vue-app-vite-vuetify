<template>
  <v-app>
    <v-main class="main">
      <Header />
      <BoxContainer />
      <Footer />
    </v-main>
  </v-app>
</template>

<script>
import BoxContainer from "./pages/BoxContainer.vue";
import Header from "./pages/Header.vue";
import Footer from "./pages/Footer.vue";

import "./App.scss";

export default {
  name: "App",

  components: {
    Header,
    BoxContainer,
    Footer,
  },

  data: () => ({
    //
  }),
};
</script>
