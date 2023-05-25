<template>
  <a-row class="header" type="flex" justify="space-between" align="middle">
    <a-col :span="6">
      <img alt="logo" src="@/assets/img/Logo.png" height="125"/>
    </a-col>
    <a-col :span="12">
      <a-menu v-model:selectedKeys="current" mode="horizontal">
        <a-menu-item key="mail"><RouterLink to="/about">Home</RouterLink></a-menu-item>
      </a-menu>
    </a-col>
  </a-row>
  <a-row>
    <a-col :span="24">
      <RouterView/>
    </a-col>
  </a-row>
  <a-row>
    <a-col :span="24">col-12</a-col>
  </a-row>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import { MailOutlined, AppstoreOutlined, SettingOutlined } from '@ant-design/icons-vue';

const current = reactive([])
</script>

<style scoped>
.header {
  /*height: 100vh;*/
  /*background-image: url("@/assets/img/HeaderBg-3840x2560.jpg");*/
//background-repeat: no-repeat; //background-size: 100% 100%;
}
</style>
