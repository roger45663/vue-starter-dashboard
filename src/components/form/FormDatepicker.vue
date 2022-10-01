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
    v-model="formModel[prop]" :clearable="false" :type="type" :placeholder="config.placeholder"
    :disabled="config.disabled" :value-format="config.valueFormat"
  />
</template>
