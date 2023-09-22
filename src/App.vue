<template>
  <v-app>
    <v-main class="container"> <dashboard></dashboard> </v-main>
  </v-app>
</template>

<script>
import dashboard from "./views/dashboard.vue";

export default {
  name: "App",

  components: {
    dashboard,
  },

  data: () => ({
    //
  }),
};
</script>
<style scoped>
.container {
  background: #898787;
}
</style>
