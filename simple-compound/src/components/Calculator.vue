<template>
  <v-container class="calculatorContainer">
    <div class="inputField">
      <div class="label">Principle amount</div>
      <v-text-field v-model="baseAmount" outlined></v-text-field>
    </div>
    <div class="inputField">
      <div class="label">Interest rate</div>
      <v-text-field v-model="interestRate" outlined>
        <v-icon slot="append" color="$grey">mdi-percent</v-icon>
      </v-text-field>
    </div>
    <div class="inputField">
      <div class="label">Calculation period</div>
      <v-row>
        <v-col>
          <v-text-field v-model="calculationPeriodValue" outlined></v-text-field>
        </v-col>
        <v-col>
          <v-btn-toggle v-model="selectedCalculationPeriodTypeValue" mandatory>
            <v-btn value="1">Years</v-btn>
            <v-btn value="12">Months</v-btn>
          </v-btn-toggle>
        </v-col>
      </v-row>
    </div>
    <div class="inputField">
      <div class="label">Compound interval</div>
      <v-overflow-btn :items="dropdownCalculationPeriodOptions" item-text="name" item-value="value" v-model="calculationPeriodInterval"></v-overflow-btn>
    </div>
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

<style lang="scss">

$grey: #50514F;

.calculatorContainer {
  color: $grey;
  .resultsSection {
    margin-top: 3%;
  }
  .label {
    font-size: 1em;
    color: $grey;
  }
  .inputField {
    margin-top: 3%;
    .col {
      padding-top: 0px;
    }
  }
}
</style>
