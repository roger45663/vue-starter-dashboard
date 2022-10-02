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
const { on, instanceRef } = toRefs(props.config)
const formModel = useVModel(props, 'model', emit)
const selectRef = ref(null)
watch(selectRef, (ins) => {
  if (!instanceRef || !ins)
    return

  instanceRef.value = ins
})
</script>

<template>
  <el-select
    ref="selectRef" v-model="formModel[prop]" :multiple="config.multiple" :disabled="config.disabled"
    :value-key="config.valueKey" :size="config.size" :clearable="config.clearable" :collapse-tags="config.collapseTags"
    :collapse-tags-tooltip="config.collapseTagsTooltip" :multiple-limit="config.multipleLimit" :name="config.name"
    :effect="config.effect" :autocomplete="config.autocomplete" :placeholder="config.placeholder"
    :filterable="config.filterable" :allow-create="config.allowCreate" :filter-method="config.filterMethod"
    :remote="config.remote" :remote-method="config.remoteMethod" :remote-show-suffix="config.remoteShowSuffix"
    :loading="config.loading" :loading-text="config.loadingText" :no-match-text="config.noMatchText"
    :no-data-text="config.noDataText" :popper-class="config.popperClass" :reserve-keyword="config.reserveKeyword"
    :default-first-option="config.defaultFirstOption" :teleported="config.teleported" :persistent="config.persistent"
    :automatic-dropdown="config.automaticDropdown" :clear-icon="config.clearIcon"
    :fit-input-width="config.fitInputWidth" :suffix-icon="config.suffixIcon"
    :suffix-transition="config.suffixTransition" :tag-type="config.tagType" :validate-event="config.validateEvent"
    :placement="config.placement" @change="on?.change" @visible-change="on?.visibleChange" @remove-tag="on?.removeTag"
    @clear="on?.clear" @blur="on?.blur" @focus="on?.focus"
  >
    <template v-for="option in config.options" :key="option.value">
      <el-option :label="option.label" :value="option.value" :disabled="option.disabled" />
    </template>
  </el-select>
</template>

<style lang="scss" scoped>
.el-select {
  width: 100%;
}
</style>
