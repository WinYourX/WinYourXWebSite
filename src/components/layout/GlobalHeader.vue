<template>
  <a-row type="flex" justify="space-between" align="middle">
    <a-col :xs="24" :sm="8" :md="8" :lg="8" :xl="6" :xxl="6" :xxxl="4">
      <RouterLink to="/"><img alt="logo" src="@/assets/img/Logo.png" height="125"/></RouterLink>
    </a-col>
    <a-col :xs="24" :sm="16" :md="16" :lg="12" :xl="12" :xxl="12" :xxxl="12">
      <TopMenu/>
    </a-col>
  </a-row>
</template>

<script setup lang="ts">
import TopMenu from "@/components/TopMenu.vue";
import {RouterLink} from "vue-router";
</script>


<style scoped>

</style>
