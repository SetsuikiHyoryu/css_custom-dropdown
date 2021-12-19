<script lang="ts" setup>
import { computed } from 'vue'
import { articles } from '../assets/data'
import { ArticleInterface } from '../typings'

interface Props {
  id: number
}

const props = defineProps<Props>()

const visibleArticle = computed(() => {
  return articles.find((item: ArticleInterface) => item.id === props.id)?.body
})
</script>

<template>
  <div id="article" v-html="visibleArticle"></div>
</template>

<style scoped></style>
