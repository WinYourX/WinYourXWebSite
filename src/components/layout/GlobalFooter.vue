<template>
  <a-row type="flex" justify="space-around" align="middle" :gutter="[16, 16]">
    <a-col
      style="text-align: center"
      v-for="item in items"
      :key="item"
      :xs="12"
      :sm="12"
      :md="8"
      :lg="6"
      :xl="6"
      :xxl="4"
      :xxxl="4"
    >
      友情链接 - {{ item.toString().padStart(2, '0') }}
    </a-col>
  </a-row>
</template>

<script setup>
import { ref } from 'vue'

const items = ref(24)
</script>

<style scoped></style>
