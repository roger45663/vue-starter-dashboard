<script setup lang="ts">
const props = defineProps({
  type: {
    type: String,
    default: 'text',
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
  <el-input
    v-model.trim="formModel[prop]" :type="type" :placeholder="config.placeholder" :rows="config.rows"
    :disabled="config.disabled" :show-password="config.showPassword" :resize="config.resize || 'none'"
  />
</template>
