<template>
  <v-card>
    <v-card-title class="purple--text">
      Monthly Expenses
    </v-card-title>
    <v-card-text>
      <v-simple-table :height="200">
        <template v-slot:default>
          <thead>
            <tr>
              <th>Name</th>
              <th>Amount</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="expense in expenses" :key="expense.name">
              <td>{{ expense.name }}</td>
              <td>${{ expense.amount }}</td>
              <td class="text-right">
                <v-btn
                  fab
                  x-small
                  color="red"
                  dark
                  @click="handleRemove(expense)"
                >
                  <v-icon>mdi-minus</v-icon>
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      <v-divider></v-divider>
      <h4 class="my-3">Add Expense</h4>
      <v-form @submit.prevent="handleSubmit">
        <v-row>
          <v-col :sm="5">
            <v-text-field
              v-model="name"
              color="purple"
              outlined
              filled
              dense
              placeholder="Expense Name"
            />
          </v-col>
          <v-col :sm="5">
            <v-text-field
              v-model="amount"
              type="number"
              color="purple"
              outlined
              filled
              dense
              placeholder="Amount"
              prefix="$"
            />
          </v-col>
          <v-col :sm="2">
            <v-btn fab small color="purple" dark type="submit">
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["expenses"],
  data() {
    return {
      name: "",
      amount: null
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("expense-added", { name: this.name, amount: +this.amount });
      this.name = "";
      this.amount = null;
    },
    handleRemove(expense) {
      this.$emit("expense-removed", expense);
    }
  }
};
</script>

<style></style>
