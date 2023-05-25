<template>
  <a-menu v-model:selectedKeys="current" mode="horizontal">
    <a-menu-item v-for="item in menuList" :key="item.key">
      <RouterLink :to="item.to">{{ item.title }}</RouterLink>
    </a-menu-item>
  </a-menu>
</template>

<script setup lang="ts">
import {ref} from 'vue'
import {RouterLink, useRoute} from "vue-router"

const route = useRoute()
const current = ref([route.name === undefined ? 'index' : route.name])
const menuList = ref([
  {
    key: 'index',
    to: '/',
    title: '首页'
  },
  {
    key: 'about',
    to: '/about',
    title: '关于'
  }
])
</script>

<style scoped>

</style>
