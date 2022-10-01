<script setup lang="ts">
const props = defineProps({
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
  <el-select
    v-model="formModel[prop]" :placeholder="config.placeholder" :rows="config.rows"
    :disabled="config.disabled"
  >
    <template v-for="option in config.options" :key="option.value">
      <el-option :label="option.label" :value="option.value" />
    </template>
  </el-select>
</template>
