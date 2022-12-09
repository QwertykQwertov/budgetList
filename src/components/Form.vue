<template>
  <ElCard class="form-card">
    <ElForm :model="store.formData" ref="addItemForm" :rules="rules" lable-position="top">
      <ElFormItem label="Тип" prop="type">
        <ElSelect class="type-select" v-model="store.formData.type" placeholder="">
          <ElOption label="Доход" value="INCOME" />
          <ElOption label="Расход" value="OUTCOME" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Комментарий" prop="comment">
        <ElInput v-model="store.formData.comment" />
      </ElFormItem>
      <ElFormItem label="Сумма" prop="value">
        <ElInput v-model.number="store.formData.value" />
      </ElFormItem>
      <ElButton @click="onSubmit()" type="primary">Добавить</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
import store from "../store"
export default {
  name: "Form",
  data: () => ({
    store,
    rules: {
      type: [
        { required: true, message: "Пожалуйста, укажите тип", trigger: "blur" }
      ],
      comment: [
        { required: true, message: "Пожалуйста, введите комментарий", trigger: "change" }
      ],
      value: [
        { required: true, message: "Пожалуйста, укажите сумму", trigger: "change" },
        { type: "number", message: "Сумма должна быть числом", trigger: "change" }
      ],

    }
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
         this.store.formData.value = this.store.formData.type === "OUTCOME" && this.store.formData.value > 0 ? 0 - this.store.formData.value : this.store.formData.value
         this.store.formData.value = this.store.formData.type === "INCOME" && this.store.formData.value < 0 ? 0 - this.store.formData.value : this.store.formData.value
          this.$emit("submitForm", { ...this.store.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    }
  }
};
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}
.type-select {
  width: 100%;
}
</style>