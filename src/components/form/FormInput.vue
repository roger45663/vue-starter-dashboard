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
  <template v-if="type !== 'number'">
    <el-input
      v-model.trim="formModel[prop]" :type="type" :maxlength="config.maxlength" :minlength="config.minlength"
      :show-word-limit="config.showWordLimit" :placeholder="config.placeholder" :clearable="config.clearable"
      :formatter="config.formatter" :parser="config.parser" :show-password="config.showPassword"
      :disabled="config.disabled" :size="config.size" :prefix-icon="config.prefixIcon" :suffix-icon="config.suffixIcon"
      :rows="config.rows" :autosize="config.autosize" :autocomplete="config.autocomplete" :name="config.name"
      :readonly="config.readonly" :resize="config.resize || 'none'" :autofocus="config.autofocus" :form="config.form"
      :label="config.label" :tabindex="config.tabindex" :validate-event="config.validateEvent"
      :input-style="config.inputStyle"
    />
  </template>
  <template v-else>
    <el-input
      v-model.trim.number="formModel[prop]" :type="type" :maxlength="config.maxlength"
      :minlength="config.minlength" :show-word-limit="config.showWordLimit" :placeholder="config.placeholder"
      :clearable="config.clearable" :disabled="config.disabled" :size="config.size" :prefix-icon="config.prefixIcon"
      :suffix-icon="config.suffixIcon" :autocomplete="config.autocomplete" :name="config.name"
      :readonly="config.readonly" :max="config.max" :min="config.min" :step="config.step" :autofocus="config.autofocus"
      :form="config.form" :label="config.label" :tabindex="config.tabindex" :validate-event="config.validateEvent"
      :input-style="config.inputStyle"
    />
  </template>
</template>
