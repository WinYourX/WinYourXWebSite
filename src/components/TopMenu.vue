<template>
  <a-menu v-model:selectedKeys="current" mode="horizontal">
    <a-menu-item v-for="item in menuList" :key="item.key">
      <RouterLink :to="item.to">{{ item.title }}</RouterLink>
    </a-menu-item>
  </a-menu>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import { RouterLink, useRoute } from 'vue-router'

const route = useRoute()
const current = ref([])
const menuList = ref([
  {
    key: 'index',
    to: '/',
    title: '首页'
  },
  {
    key: 'gasp',
    to: '/gasp',
    title: 'Gasp'
  },
  {
    key: 'threejs',
    to: '/threejs',
    title: 'ThreeJs'
  },
  {
    key: 'about',
    to: '/about',
    title: '关于'
  }
])

watch(
  () => route.name,
  (newValue, oldValue) => {
    current.value = [newValue]
  }
)
</script>

<style scoped></style>
