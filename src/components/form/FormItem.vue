<script setup lang="ts">
defineProps({
  config: {
    type: Object,
    default: () => ({}),
  },
})
</script>

<template>
  <el-form-item
    :label="config.label" :prop="config.prop" :rules="config.rules"
    :size="config.size" :class="config.class"
  >
    <slot />
  </el-form-item>
</template>

