<template>
  <div
    class="total-value"
    :style="{ color: setColor }"
  >Баланс: {{ totalBalance + ' ₽'}}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: ['listItem'],
  computed: {
    totalBalance () {
      return Object.values(this.listItem).reduce((acc, el) => acc + el.value, 0)
    },
    setColor () {
      if (!this.totalBalance) {
        return 'black'
      } else {
        return this.totalBalance > 0? 'green' : 'red'
      }
      
    }
  }
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>