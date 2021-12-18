<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Selector from './components/Selector.vue'
import Article from './components/Article.vue'

const titleList: string[] = [
  '共產黨宣言',
  '尋烏調查',
  '紀念白求恩',
  '爲人民服務',
  '愚公移山',
]
</script>

<template>
  <Selector :list="titleList" />
  <Article :id="2" />
</template>

<style></style>
