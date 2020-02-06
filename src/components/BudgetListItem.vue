<template>
  <div class="list-item">
    <span class="budget-comment">{{ item.comment }}</span>
    <span class="budget-value">{{ item.value }}</span>
    <el-button type="danger" size="mini" @click="deleteItem(item.id)">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    }
  },
  props: {
    item: {
      type: Object,
      default: () => ({})
    }
  },

}
</script>

<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  margin-left: auto;
  font-weight: 600;
  margin-right: 20px;
}
</style>