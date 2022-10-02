<script setup lang="ts">
/**
 * TODO:
 * 讓使用這可以新增自定義的component，ex: {component: MyComponent}
 */
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
      labelPosition: 'top',
    },
  },
  items: [
    {
      span: 8,
      prop: 'name',
      type: 'text',
      label: '姓名',
      placeholder: '請輸入',
      rules: [
        {
          required: true,
          message: '请输入',
          trigger: 'blur',
        },
      ],
    },
    {
      span: 8,
      prop: 'number',
      type: 'number',
      label: '數字',
      placeholder: '請輸入',
      rules: [
        {
          required: true,
          message: '请输入',
          trigger: 'blur',
        },
      ],
    },
    {
      span: 8,
      prop: 'email',
      type: 'email',
      label: '信箱',
      placeholder: '請輸入',
      rules: [
        {
          required: true,
          message: '请输入',
          trigger: 'blur',
        },
      ],
    },
    {
      span: 8,
      prop: 'tel',
      type: 'tel',
      label: '電話',
      placeholder: '請輸入',
      rules: [
        {
          required: true,
          message: '请输入',
          trigger: 'blur',
        },
      ],
    },
    {
      span: 8,
      prop: 'textarea',
      type: 'textarea',
      label: '備註',
      placeholder: '請輸入',
      rows: 4,
      rules: [
        {
          required: true,
          message: '请输入',
          trigger: 'blur',
        },
      ],
    },
    {
      span: 8,
      prop: 'select',
      type: 'select',
      label: '選擇',
      placeholder: '請選擇',
      clearable: true,
      options: [
        {
          label: '選項一',
          value: '1',
        }, {
          label: '選項二',
          value: '2',
        },
      ],
      rules: [
        {
          required: true,
          message: '请選擇',
          trigger: 'change',
        },
      ],
    },
    {
      span: 8,
      prop: 'select2',
      type: 'select',
      label: '選擇2',
      placeholder: '請選擇',
      multiple: true,
      filterable: true,
      instanceRef: null,
      allowCreate: true,
      options: [
        {
          label: '選項一',
          value: '1',
        }, {
          label: '選項二',
          value: '2',
        },
      ],
      rules: [
        {
          required: true,
          message: '请選擇',
          trigger: 'change',
        },
      ],
    },
    // {
    //   span: 12,
    //   prop: 'date',
    //   children: {
    //     config: {
    //       row: {
    //         gutter: 32,
    //         justify: 'start',
    //         align: 'top',
    //         tag: 'div',
    //       },
    //       form: {
    //         size: 'large',
    //       },
    //     },
    //     items: [
    //       {
    //         span: 12,
    //         prop: 'name2',
    //         type: 'text',
    //         label: '姓名2',
    //         placeholder: '請輸入',
    //         rules: [
    //           {
    //             required: true,
    //             message: '请输入名称',
    //             trigger: 'blur',
    //           },
    //         ],
    //       },
    //       {
    //         span: 12,
    //         prop: 'select2',
    //         type: 'select',
    //         label: '選擇2',
    //         placeholder: '請選擇',
    //         options: [
    //           {
    //             label: '選項一',
    //             value: '1',
    //           }, {
    //             label: '選項二',
    //             value: '2',
    //           },
    //         ],
    //       },
    //       {
    //         span: 12,
    //         prop: 'date',
    //         type: 'date',
    //         label: '日期',
    //         placeholder: '請輸入',
    //         rules: [
    //           {
    //             required: true,
    //             message: '请输入名称',
    //             trigger: 'blur',
    //           },
    //         ],
    //       },
    //     ],
    //   },
    // },
  ],
})
const formModel = reactive({
  name: '',
})
</script>

<template>
  <el-container p="20px">
    <FormItems wrap-by-form :config="formConfig" :model="formModel" />
  </el-container>
</template>
