<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <input
        type="radio"
        value="ALL"
        v-model="store.picked"
        @change="filterList"
      />
      <label for="one">Все</label>

      <input
        type="radio"
        value="INCOME"
        v-model="store.picked"
        @change="filterList"
      />
      <label for="two">Доходы</label>

      <input
        type="radio"
        value="OUTCOME"
        v-model="store.picked"
        @change="filterList"
      />
      <label for="two">Расходы</label>

      <template v-if="!isEmpty">
        <BudgetListItem
          :list="list"
          :picked="store.picked"
          @deleteItem="this.deleteItem"
        />
      </template>
      <ElAlert
        v-else
        type="info"
        :title="emptyTitle"
        :closable="false"
      />
    </ElCard>
  </div>
</template>

<script>
import BudgetListItem from "./BudgetListItem.vue"
import store from "../store"
export default {
  name: "BudgetList",
  components: {
    BudgetListItem
  },
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    store,
    header: "Доходы и расходы",
    emptyTitle: "Список пуст",
  }),
  mounted () {
    this.filterList(this.store.picked)
  },
  computed: {
    isEmpty () {
      return !Object.keys(this.store.list).length;
    }
  },
  methods: {
    deleteItem (id) {
      this.$emit("deleteItem", id);
    },
    filterList () {
      this.store.sortList = { ...this.store.list }

      if (this.store.picked === "ALL") {
        this.store.sortList = this.store.list
      } else {
        for (let item of Object.values(this.store.sortList)) {
          if (item.type !== this.store.picked) {
            this.$delete(this.store.sortList, item.id)
          }
        }
      }
    }
  }
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
</style>