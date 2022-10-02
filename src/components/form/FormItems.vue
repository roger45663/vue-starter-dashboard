<script setup lang="ts">
import { ElForm } from 'element-plus'
const props = defineProps({
  wrapByForm: {
    type: Boolean,
    default: false,
  },
  model: {
    type: Object,
    default: () => ({}),
  },
  config: {
    type: [Array, Object],
    default: () => (reactive({})),
  },
})
const emit = defineEmits(['update:model'])
const { wrapByForm } = toRefs(props)
const { items, config } = toRefs(props.config)
const { row, form } = toRefs(config.value)
const rootOfWrapper = computed(() => wrapByForm ? ElForm : 'div')
const formRef = ref(null)
const formModel = useVModel(props, 'model', emit)
const formConfig = computed(() => {
  return {
    inline: wrapByForm ? (form && form.value.inline) || false : '',
    labelPosition: wrapByForm ? (form && form.value.labelPosition) || 'right' : '',
    labelWidth: wrapByForm ? (form && form.value.labelWidth) || '80px' : '',
    requireAsteriskPosition: wrapByForm ? (form && form.value.requireAsteriskPosition) || 'right' : '',
    size: wrapByForm ? (form && form.value.size) || 'default' : '',
    disabled: wrapByForm ? (form && form.value.disabled) || false : '',
    scrollToError: wrapByForm ? (form && form.value.scrollToError) || false : '',
    class: (form && form.value.class) || '',
  }
})
const rowConfig = computed(() => {
  return {
    gutter: (row && row.value.gutter) || 32,
    justify: (row && row.value.justify) || 'start',
    align: (row && row.value.align) || 'top',
    tag: (row && row.value.tag) || 'div',
  }
})
</script>

<template>
  <component
    :is="rootOfWrapper" ref="formRef" :model="formModel" :inline="formConfig.inline"
    :label-position="formConfig.labelPosition" :label-width="formConfig.labelWidth"
    :require-asterisk-position="formConfig.requireAsteriskPosition" :size="formConfig.size"
    :disabled="formConfig.disabled" :scroll-to-error="formConfig.scrollToError" :class="formConfig.class"
    w="100%"
  >
    <el-row :gutter="rowConfig.gutter" :justify="rowConfig.justify" :align="rowConfig.align" :tag="rowConfig.tag">
      <template v-for="(item, index) in items" :key="index">
        <template v-if="item.isShow !== undefined ? item.isShow : true">
          <el-col
            :span="item.span" :offset="item.offset" :push="item.push" :pull="item.pull"
            :xs="item.xs" :sm="item.sm" :md="item.md" :lg="item.lg" :xl="item.xl"
            :tag="item.tag"
          >
            <FormItem :config="item">
              <template v-if="!item.children">
                <template
                  v-if="item.type === 'text' || item.type === 'textarea' || item.type === 'password' || item.type === 'tel' || item.type === 'number' || item.type === 'email'"
                >
                  <FormInput :type="item.type" :model="formModel" :config="item" :prop="item.prop" />
                </template>
                <template v-if="item.type === 'select'">
                  <FormSelect :model="formModel" :config="item" :prop="item.prop" />
                </template>
                <template v-if="item.type === 'radio' || item.type === 'radio-button'">
                  <FormRadio :type="item.type" :model="formModel" :config="item" :prop="item.prop" />
                </template>
                <template v-if="item.type === 'checkbox' || item.type === 'checkbox-group'">
                  <FormCheckbox :type="item.type" :model="formModel" :config="item" :prop="item.prop" />
                </template>
                <template v-if="item.type === 'date'">
                  <FormDatepicker :type="item.type" :model="formModel" :config="item" :prop="item.prop" />
                </template>
              </template>

              <template v-if="item.children && item.children.items && item.children.items.length">
                <FormItems :config="item.children" :model="formModel" />
              </template>
            </FormItem>
          </el-col>
        </template>
      </template>
    </el-row>
  </component>
</template>

<style lang="scss" scoped>
.el-col {
  &:not(:last-child) {
    margin-bottom: 20px;
  }
}
</style>

