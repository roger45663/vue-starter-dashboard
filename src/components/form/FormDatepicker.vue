<script setup lang="ts">
const props = defineProps({
  type: {
    type: String,
    default: 'date',
  },
  model: {
    type: Object,
    default: () => ({}),
  },
  config: {
    type: Object,
    default: () => ({}),
  },
  prop: {
    type: String,
    default: '',
  },
})
const emit = defineEmits(['update:model'])
const formModel = useVModel(props, 'model', emit)
</script>

<template>
  <el-date-picker
    v-model="formModel[prop]" :type="type" :clearable="config.clearable" :placeholder="config.placeholder"
    :disabled="config.disabled" :value-format="config.valueFormat"
  />
</template>

<style lang="scss">
.el-date-editor {
  width: 100% !important;

  .el-input__wrapper {
    width: 100%;
  }

}
</style>
