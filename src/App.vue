<template>
  <a-space direction="vertical" style="width: 100vw">
    <div class="header">
      <GlobalHeader />
    </div>
    <div class="body">
      <a-row>
        <a-col :span="24">
          <RouterView />
        </a-col>
      </a-row>
    </div>
    <div class="footer">
      <GlobalFooter />
    </div>
  </a-space>
</template>

<script setup lang="ts">
import GlobalHeader from '@/components/layout/GlobalHeader.vue'
import GlobalFooter from '@/components/layout/GlobalFooter.vue'
</script>

<style scoped>
.header {
  width: 96vw;
  margin: 0 auto;
  border-bottom: #d5eaff 1px solid;
  /*background-image: url("@/assets/img/HeaderBg-3840x2560.jpg");*/
  //background-repeat: no-repeat; //background-size: 100% 100%;
}

.body {
  width: 90vw;
  margin: 0 auto;
  min-height: 50vh;
}

.footer {
  width: 100vw;
  margin: 0 auto;
  background-image: linear-gradient(0deg, #fff, #d5eaff);
  padding-top: 30px;
  min-height: 30vh;
}
</style>
