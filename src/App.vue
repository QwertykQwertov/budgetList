<template>
  <div id="app">
    <Form @submitForm="onFormSubmit" />
    <TotalBalance :listItem="store.list"/>
    <BudgetList 
      ref="refBudgetList"
      @deleteItem="onDeleteItem"
    />
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";
import store from "./store"

export default {
  name: "app",
  data: ()=> ({
    store,
  }),
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  
  methods: {
    onDeleteItem (id) {
      this.$delete(this.store.list, id);
    },
    onFormSubmit (data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };

      this.$set(this.store.list, newObj.id, newObj);
      this.$refs.refBudgetList.filterList()
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
