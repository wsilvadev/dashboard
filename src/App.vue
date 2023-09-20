<template>
  <v-app>
    <v-main class="container">
      <card-dashboard
        title="Saldo total"
        :value="303524"
        :isSubscribers="true"
      />
      <card-dashboard
        title="Saldo total"
        :value="24545234"
        :isSubscribers="false"
      />
      <card-dashboard
        title="Saldo total"
        :value="423452"
        :isSubscribers="true"
      />
      <card-dashboard
        title="Saldo total"
        :value="24345234"
        :isSubscribers="false"
      />
      <card-dashboard
        title="Saldo total"
        :value="24525234"
        :isSubscribers="false"
      />
    </v-main>
  </v-app>
</template>

<script>
import cardDashboard from "./components/CardDashboard.vue";

export default {
  name: "App",

  components: {
    cardDashboard,
  },

  data: () => ({
    //
  }),
};
</script>
<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.v-main__wrap {
  flex: 0;
}
</style>
