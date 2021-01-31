<template>
  <v-card height="100%">
    <v-card-title class="purple--text">Monthly Expense Breakdown</v-card-title>
    <apexchart type="pie" :options="options" :series="series" height="300" />
  </v-card>
</template>

<script>
export default {
  props: ["expenses", "totalAmount"],
  computed: {
    series() {
      return this.expenses.map(e => e.amount);
    },
    options() {
      return {
        labels: this.expenses.map(e => e.name)
      };
    }
  }
};
</script>

<style></style>
