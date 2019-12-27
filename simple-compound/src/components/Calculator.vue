<template>
  <v-container>
    <v-text-field label="Base amount" v-model="baseAmount"></v-text-field>
    <v-text-field label="Interest rate" v-model="interestRate">
      <v-icon slot="append" color="green">mdi-percent</v-icon>
    </v-text-field>
    <v-text-field label="Calculation period" v-model="calculationPeriod"></v-text-field>
    <v-overflow-btn :items="dropdownCalculationPeriodOptions" label="Compound interval"></v-overflow-btn>
    <v-text-field label="Regular monthly deposit" v-model="regularDeposit"></v-text-field>
    {{ result }}
  </v-container>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    baseAmount: 0,
    interestRate: 0,
    calculationPeriod: 0,
    dropdownCalculationPeriodOptions: ['Daily', 'Monthly', 'Quarterly', 'Half yearly', 'Yearly'],
    regularDeposit: 0
  }),
  computed: {
    result () {
      return (this.baseAmount * Math.pow((1 + (this.interestRate / 100)), this.calculationPeriod)).toFixed(2)
    }
  }
}
</script>
