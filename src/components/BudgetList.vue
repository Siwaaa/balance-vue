<template>
  <div class="budget-list-wrap">
    <el-card :header="header">
      <template v-if="isEmpty">
        <!-- Перебираем значение и свойство -->
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-comment">{{ item.comment }}</span>
          <span class="budget-value">{{ item.value }}</span>
          <el-button type="danger" size="mani" @click="deleteItem(item.id)">Delete</el-button>
        </div>
      </template>
      <el-alert v-else type="info" :title="emptyTitle" :closable="false"></el-alert>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "BudgetList",
  data: () => ({
    header: "Budget List",
    emptyTitle: "Лист пуст",
  }),
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {
    isEmpty() {
      return Boolean(Object.keys(this.list).length);
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id)
    }
  }
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>