<template>
  <v-container>
    <v-text-field label="Principle amount" v-model="baseAmount"></v-text-field>
    <v-text-field label="Interest rate" v-model="interestRate">
      <v-icon slot="append" color="black">mdi-percent</v-icon>
    </v-text-field>
    <v-container>
      <v-row>
        <v-text-field label="Calculation period" v-model="calculationPeriodValue"></v-text-field>
        <v-btn-toggle v-model="selectedCalculationPeriodTypeValue" mandatory>
          <v-btn value="1">Years</v-btn>
          <v-btn value="12">Months</v-btn>
        </v-btn-toggle>
      </v-row>
    </v-container>
    <div>Compound interval</div>
    <v-overflow-btn :items="dropdownCalculationPeriodOptions" item-text="name" item-value="value" label="Compound interval" v-model="calculationPeriodInterval"></v-overflow-btn>
    <div class="resultsSection">
      <div>Total balance: {{ result }}</div>
      <div>Total interest earned: {{ totalInterest }}</div>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    baseAmount: 0,
    interestRate: 0,
    calculationPeriodValue: 0,
    calculationPeriodInterval: 1,
    selectedCalculationPeriodTypeValue: '1',
    dropdownCalculationPeriodOptions:
    [
      {
        name: 'Daily',
        value: 365
      },
      {
        name: 'Monthly',
        value: 12
      },
      {
        name: 'Quarterly',
        value: 4
      },
      {
        name: 'Half yearly',
        value: 2
      },
      {
        name: 'Yearly',
        value: 1
      }
    ]
  }),
  computed: {
    calculationPeriod () {
      return this.calculationPeriodValue / this.selectedCalculationPeriodTypeValue
    },
    depositTotal () {
      return this.calculationPeriodInterval * this.calculationPeriod
    },
    result () {
      return (parseInt(this.baseAmount) * Math.pow((1 + ((this.interestRate / 100) / this.calculationPeriodInterval)), (this.calculationPeriodInterval * this.calculationPeriod))).toFixed(2)
    },
    totalInterest () {
      return (this.result - this.baseAmount).toFixed(2)
    }
  }
}
</script>

<style lang="scss" scoped>
.resultsSection {
  margin-top: 5%;
}
</style>
