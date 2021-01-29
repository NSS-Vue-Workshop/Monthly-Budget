<template>
  <v-card height="100%">
    <v-card-title class="purple--text">{{ title }}</v-card-title>
    <v-card-text>
      <h1 class="net-amount pb-5" :class="dollarClass">{{ displayAmount }}</h1>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["title", "netAmount"],
  computed: {
    dollarClass() {
      return {
        "green--text": this.netAmount >= 0,
        "red--text": this.netAmount < 0
      };
    },
    displayAmount() {
      return new Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "USD"
      }).format(this.netAmount);
    }
  }
};
</script>

<style scoped>
.net-amount {
  font-size: 4em;
  margin-top: 20px;
  text-align: center;
}
</style>
