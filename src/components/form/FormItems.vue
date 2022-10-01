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
  >
    <el-row :gutter="rowConfig.gutter" :justify="rowConfig.justify" :align="rowConfig.align" :tag="rowConfig.tag">
      <template v-for="(item, index) in items" :key="index">
        <template v-if="item.col.isShow !== undefined ? item.col.isShow : true">
          <el-col
            :span="item.col.span" :offset="item.col.offset" :push="item.col.push" :pull="item.col.pull"
            :xs="item.col.xs" :sm="item.col.sm" :md="item.col.md" :lg="item.col.lg" :xl="item.col.xl"
            :tag="item.col.tag"
          >
            <FormItem :config="item.formItem">
              <template v-if="!item.form.children">
                <template
                  v-if="item.form.type === 'text' || item.form.type === 'textarea' || item.form.type === 'password' || item.form.type === 'tel' || item.form.type === 'number' || item.form.type === 'email'"
                >
                  <FormInput :type="item.form.type" :model="formModel" :config="item.form" :prop="item.formItem.prop" />
                </template>
                <template v-if="item.form.type === 'select'">
                  <FormSelect :model="formModel" :config="item.form" :prop="item.formItem.prop" />
                </template>
                <template v-if="item.form.type === 'radio' || item.form.type === 'radio-button'">
                  <FormRadio :type="item.form.type" :model="formModel" :config="item.form" :prop="item.formItem.prop" />
                </template>
                <template v-if="item.form.type === 'checkbox' || item.form.type === 'checkbox-group'">
                  <FormCheckbox :type="item.form.type" :model="formModel" :config="item.form" :prop="item.formItem.prop" />
                </template>
                <template v-if="item.form.type === 'date'">
                  <FormDatepicker :type="item.form.type" :model="formModel" :config="item.form" :prop="item.formItem.prop" />
                </template>
              </template>

              <template v-if="item.form.children && item.form.children.items && item.form.children.items.length">
                <FormItems :config="item.form.children" :model="formModel" />
              </template>
            </FormItem>
          </el-col>
        </template>
      </template>
    </el-row>
  </component>
</template>

