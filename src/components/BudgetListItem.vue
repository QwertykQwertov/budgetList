 /* eslint-disable */
<template>
  <div>
    <div
      class="list-item"
      v-for="(item, id) in store.sortList"
      :key="id"
    >
        <i :class="item.type === 'INCOME' ? 'el-icon-top' : 'el-icon-bottom'" />

        <span class="budget-comment">{{ item.comment }}</span>
        <span
          class="budget-value"
          :style="{color: (item.type === 'INCOME') ? 'green' : 'red' }"
        >{{ item.value + ' ₽' }}</span>
        <ElButton
          type="danger"
          size="mini"
          @click="deleteItem(item.id)"
        >Удалить</ElButton>
    </div>
  </div>
</template>


<script>
import store from "../store"
export default {
  name: "BudgetList",
  data () {
    return {
      store
    }
  },
  computed: {
    isEmpty () {
      return !Object.keys(this.store.list).length;
    }
  },
  methods: {
    deleteItem (id) {
      let realDelete = confirm("Вы уверены, что хотите удалить элемент из списка?")
      if (realDelete) this.$emit("deleteItem", id);
    },

  }
};
</script>
<style scoped>
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