<script setup lang="ts">
import { ElCheckboxGroup } from 'element-plus'
const props = defineProps({
  type: {
    type: String,
    default: 'checkbox',
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
const { prop, type, config } = toRefs(props)
const formModel = useVModel(props, 'model', emit)
const wrapOfCheckbox = computed(() => props.type === 'checkbox-group' ? ElCheckboxGroup : 'div')
const isCheckboxGroup = computed(() => type.value === 'checkbox-group')
const vModelOfWrapper = computed(() => isCheckboxGroup ? formModel.value[prop.value] : '')
const disabledOfWrapper = computed(() => isCheckboxGroup ? config.value.disabled : '')
const vModelOfCheckbox = computed(() => !isCheckboxGroup ? formModel.value[prop.value] : '')
const disabledOfCheckbox = computed(() => !isCheckboxGroup ? config.value.disabled : '')
</script>

<template>
  <component :is="wrapOfCheckbox" v-model="vModelOfWrapper" :disabled="disabledOfWrapper">
    <template v-for="option in config.options" :key="option.label">
      <el-checkbox v-model="vModelOfCheckbox" :label="option.value" :disabled="disabledOfCheckbox">
        {{ option.label }}
      </el-checkbox>
    </template>
  </component>
</template>
