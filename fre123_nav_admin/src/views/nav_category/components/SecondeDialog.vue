<template>
  <el-dialog :model-value="visible" @close="handleClose">
    <template #header>
      {{ dialogHeader }}
    </template>
    <el-form
      :model="formData"
      class="demo-form-inline"
      :rules="rules.baseRules"
      label-width="auto"
      ref="newCategoryForm_second"
    >
      <el-form-item label="类别名称" prop="tab_name" class="form-top">
        <el-input v-model="formData.tab_name" clearable />
      </el-form-item>

      <el-form-item label="右侧广告文本">
        <el-input v-model="formData.upper_right_corner.title" clearable />
      </el-form-item>
      <el-form-item label="右侧广告地址">
        <el-input v-model="formData.upper_right_corner.url" clearable />
      </el-form-item>

      <el-form-item class="close">
        <el-button
          v-if="editMode"
          type="primary"
          @click="onSubmit(newCategoryForm_second)"
          style="margin-left: 80%"
          >确认修改</el-button
        >
        <el-button
          v-else
          type="primary"
          @click="onSubmitNew(newCategoryForm_second)"
          style="margin-left: 80%"
          >确认新建</el-button
        >
      </el-form-item>
    </el-form>
  </el-dialog>
</template>
<script setup lang="ts">
import { ref, defineProps } from 'vue'
import { rules } from '@/views/nav_category/index'
const newCategoryForm_second = ref()
interface FormData {
  tab_name: string
  tab_name_url: string
  upper_right_corner: {
    title: string
    url: string
  }
}

const props = withDefaults(
  defineProps<{
    visible?: boolean
    dialogHeader?: string
    formData: FormData
    editMode?: boolean
  }>(),
  {
    visible: false,
  }
)

const emit = defineEmits<{
  (e: 'onSubmit', value: any): void
  (e: 'onSubmitNew', value: any): void
}>()

const resetForm = () => {
  if (newCategoryForm_second.value) {
    newCategoryForm_second.value.resetFields()
  }
}

const handleClose = () => {
  resetForm()
}

const onSubmit = (value: any) => {
  emit('onSubmit', value)
}

const onSubmitNew = (value: any) => {
  emit('onSubmitNew', value)
}
</script>

<style scoped>
.form-top {
  margin-top: 20px;
}
.demo-form-inline .el-form-item {
  margin-left: 15px;
}
.demo-form-inline .el-input {
  --el-input-width: 520px;
}
.demo-form-inline .el-select {
  --el-select-width: 520px;
}
</style>
