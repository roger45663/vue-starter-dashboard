<script setup lang="ts">
const formConfig = reactive({
  config: {
    row: {
      gutter: 32,
      justify: 'start',
      align: 'top',
      tag: 'div',
    },
    form: {
      size: 'large',
    },
  },
  items: [
    {
      col: {
        span: 12,
      },
      formItem: {
        prop: 'name',
        rules: [
          {
            required: true,
            message: '请输入名称',
            trigger: 'blur',
          },
        ],
      },
      form: {
        type: 'text',
        placeholder: '請輸入',
      },
    },
    {
      col: {
        span: 12,
      },
      formItem: {
        prop: 'select',
      },
      form: {
        type: 'select',
        placeholder: '請選擇',
        options: [
          {
            label: '選項一',
            value: '1',
          }, {
            label: '選項二',
            value: '2',
          },
        ],
      },
    },
    {
      col: {
        span: 12,
      },
      formItem: {
        prop: 'date',
      },
      form: {
        type: 'date',
        placeholder: '請選擇',
        children: {
          config: {
            row: {
              gutter: 32,
              justify: 'start',
              align: 'top',
              tag: 'div',
            },
            form: {
              size: 'large',
            },
          },
          items: [
            {
              col: {
                span: 12,
              },
              formItem: {
                prop: 'name',
                rules: [
                  {
                    required: true,
                    message: '请输入名称',
                    trigger: 'blur',
                  },
                ],
              },
              form: {
                type: 'text',
                placeholder: '請輸入',
              },
            },
            {
              col: {
                span: 12,
              },
              formItem: {
                prop: 'select',
              },
              form: {
                type: 'select',
                placeholder: '請選擇',
                options: [
                  {
                    label: '選項一',
                    value: '1',
                  }, {
                    label: '選項二',
                    value: '2',
                  },
                ],
              },
            },
          ],
        },
      },
    },
  ],
})
const formModel = reactive({
  name: '',
})
</script>

<template>
  <FormItems wrap-by-form :config="formConfig" :model="formModel" />
</template>
