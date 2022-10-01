<script setup lang="ts">
const props = defineProps({
  type: {
    type: String,
    default: 'radio',
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
  <el-radio-group v-model="formModel[prop]" :disabled="config.disabled">
    <template v-for="option in config.options" :key="option.label">
      <el-radio :label="option.value" :size="config.size" :border="type === 'radio-button'">
        {{ option.label }}
      </el-radio>
    </template>
  </el-radio-group>
</template>
