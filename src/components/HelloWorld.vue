<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>Einkommen inkl. MwSt. (€): <input v-model="income" type="number"></div>
    <div>Umsatzsteuer %: <input v-model="ustPercent" type="number"></div>
    <div>Einkommensteuer %: <input v-model="taxPercent" type="number"></div>
    <div>Sparen %: <input v-model="savingsPercent" type="number"></div>
    <div>Einkommen exkl. MwSt.: € {{ net.toLocaleString() }}</div>
    <div>Budget USt.: € <span v-bind:style="{ backgroundColor: ustColor}">{{ ust.toLocaleString() }}</span></div>
    <div>Budget EkSt.: € <span v-bind:style="{ backgroundColor: incomeTaxColor}">{{ incomeTax.toLocaleString() }}</span></div>
    <div>Gewinn: € {{ profit.toLocaleString() }}</div>
    <div>Sparen/Rücklagen: € <span v-bind:style="{ backgroundColor: savingsColor}">{{ savings.toLocaleString() }}</span></div>
    <div>Result: € <span v-bind:style="{ backgroundColor: resultColor}">{{ result.toLocaleString() }}</span></div>
    <div class="progress-bar flex-container">
      <div class="progress-bar ust" v-bind:style="{ width: (this.ust / this.income) * 100 + '%', backgroundColor: ustColor }"></div>
      <div class="progress-bar income-tax" v-bind:style="{ width: (this.incomeTax / this.income) * 100 + '%', backgroundColor: incomeTaxColor }"></div>
      <div class="progress-bar savings" v-bind:style="{ width: (this.savings / this.income) * 100 + '%', backgroundColor: savingsColor }"></div>
      <div class="progress-bar result" v-bind:style="{ width: (this.result / this.income) * 100 + '%', backgroundColor: resultColor }"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      income: 0, // default
      ustPercent: 19, // default
      taxPercent: 33, // default
      savingsPercent: 10, // default

      ustColor: 'violet',
      incomeTaxColor: 'yellow',
      savingsColor: 'lightgrey',
      resultColor: 'lightgreen',
    }
  },
  computed: {
    net() {
      return this.income / ((this.ustPercent/100) + 1)
    },
    ust() {
      return this.net * (this.ustPercent/100)
    },
    incomeTax() {
      return this.net * (this.taxPercent/100)
    },
    profit() {
      return this.net - this.incomeTax
    },
    savings() {
      return this.profit * (this.savingsPercent/100)
    },
    result() {
      return this.profit - this.savings
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
}
.flex-container {
  display: inline-flex;
  width: 100%;
}
.progress-bar {
  .background-color: black;
  height: 20px;
}
</style>
