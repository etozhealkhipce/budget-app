<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList'
import TotalBalance from '@/components/TotalBalance'
import Form from '@/components/Form'


export default {
  name: 'app',
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some comment',
        id: 2,
      }
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => (acc + item.value), 0);
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      if (newObj.type === 'OUTCOME' && Math.sign(newObj.value) === 1) {
        newObj.value = -newObj.value;
      }
      this.$set(this.list, newObj.id, newObj)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 1.2rem;
}


</style>
