<template>
  <v-container>
    <v-text-field label="Base amount" v-model="baseAmount"></v-text-field>
    <v-text-field label="Interest rate" v-model="interestRate">
      <v-icon slot="append" color="green">mdi-percent</v-icon>
    </v-text-field>
    <v-container>
      <v-row>
        <v-text-field label="Calculation period" v-model="calculationPeriodValue"></v-text-field>
        <!-- <v-overflow-btn :items="calculationPeriodTypes" item-text="name" item-value="value" v-model="selectedCalculationPeriodTypeValue"></v-overflow-btn> -->
        <v-btn-toggle v-model="selectedCalculationPeriodTypeValue">
          <v-btn value="1">Years</v-btn>
          <v-btn value="12">Months</v-btn>
        </v-btn-toggle>
      </v-row>
    </v-container>
    <v-overflow-btn :items="dropdownCalculationPeriodOptions" item-text="name" item-value="value" label="Compound interval" v-model="calculationPeriodInterval"></v-overflow-btn>
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
    calculationPeriodValue: 0,
    calculationPeriodInterval: 1,
    calculationPeriodTypes:
    [
      {
        name: 'Years',
        value: 1
      },
      {
        name: 'Months',
        value: 12
      }
    ],
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
    ],
    regularDeposit: 0
  }),
  computed: {
    calculationPeriod () {
      return this.calculationPeriodValue / this.selectedCalculationPeriodTypeValue
    },
    result () {
      return (this.baseAmount * Math.pow((1 + ((this.interestRate / 100) / this.calculationPeriodInterval)), (this.calculationPeriodInterval * this.calculationPeriod))).toFixed(2)
    }
  }
}
</script>
