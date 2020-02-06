<template>
  <div class="total-balance" :class="totalStyle">Total balance {{ total }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  computed: {
    totalStyle() {
      return {
        red: Math.sign(this.total) === -1,
        green: Math.sign(this.total) === 1,
      }
    }
  }
}
</script>

<style scoped>
.total-balance {
  font-size: 25px;
  font-weight: 600;
  margin: auto;
  margin-bottom: 1.5rem;
  margin-top: 1.5rem;
}
.red {
  color: red;
}

.green {
  color: green;
}
</style>