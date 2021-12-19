<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Selector from './components/Selector.vue'
import Article from './components/Article.vue'
import { ref } from 'vue'
import { articles } from './assets/data'
import { ArticleInterface } from './typings'

const titleList: string[] = articles.map((item: ArticleInterface) => item.title)

const selectedArticleID = ref<number>(0)
</script>

<template>
  <Selector
    :list="titleList"
    @select-article="(id: number) => selectedArticleID = id"
  />

  <Article class="article" :id="selectedArticleID" />
</template>

<style scoped>
.article {
  margin: 3rem 0 0;
}
</style>
