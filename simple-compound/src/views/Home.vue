<template>
  <div class="home">
    <Calculator/>
  </div>
</template>

<script>
// @ is an alias to /src
import Calculator from '@/components/Calculator.vue'

export default {
  name: 'home',
  components: {
    Calculator
  }
}
</script>

<style lang="scss" scoped>
.home {
  margin-top: 12px;
}
</style>
