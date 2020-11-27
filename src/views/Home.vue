<template>
  <div>
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";

export default {
  name: 'Home',
  components: {
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'sdfd',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'sdfd',
        id: 2,
      }
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((sum, item) => sum + item.value, 0)
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id)
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj)
    }
  }
}
</script>