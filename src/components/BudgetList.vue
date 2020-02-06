<template>
  <div class="budget-list-wrap">
    <el-card :header="header">
      <template v-if="isEmpty">
        <BudgetListItem :list="list" v-for="(item, prop) in list" :key="prop" :item="item" @deleteItem="deleteItem"/>
      </template>
      <el-alert v-else type="info" :closable="false" :title="emptyTitle"></el-alert>
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from '@/components/BudgetListItem'

export default {
  name: "BudgetList",
  components: {
    BudgetListItem,
  },
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: function() {
    return {
      header: "Budget List",
      emptyTitle: "Empty List"
    };
  },
  computed: {
    isEmpty() {
      return Boolean(Object.keys(this.list).length);
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    }
  }
}
</script>

<style scoped>
.budget-list-wrap {
  max-width: 40%;
  margin: auto;
}
</style>