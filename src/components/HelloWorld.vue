<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>Einkommen inkl. MwSt. (€): <input v-model="income" type="number"></div>
    <div>Umsatzsteuer %: <input v-model="ustPercent" type="number"></div>
    <div>Einkommensteuer %: <input v-model="taxPercent" type="number"></div>
    <div>Sparen %: <input v-model="savingsPercent" type="number"></div>
    <div>Budget USt.: € {{ ust.toLocaleString() }}</div>
    <div>Budget EkSt.: € {{ incomeTax.toLocaleString() }}</div>
    <div>Gewinn: € {{ profit.toLocaleString() }}</div>
    <div>Sparen/Rücklagen: € {{ savings.toLocaleString() }}</div>
    <div>Result: € {{ result.toLocaleString() }}</div>
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
      income: 0,
      ustPercent: 19,
      taxPercent: 33,
      savingsPercent: 10,
    }
  },
  computed: {
    net() {
      return this.income / ('1.' + this.ustPercent)
    },
    ust() {
      return this.net * ('.' + this.ustPercent)
    },
    incomeTax() {
      return this.net * ('.' + this.taxPercent)
    },
    profit() {
      return this.net - this.incomeTax
    },
    savings() {
      return this.profit * ('.' + this.savingsPercent)
    },
    result() {
      return this.profit - this.savings
    }
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
</style>
