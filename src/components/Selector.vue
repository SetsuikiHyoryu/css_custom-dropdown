<script setup lang="ts">
interface Props {
  list: string[]
}

const props = defineProps<Props>()
</script>

<template>
  <div>{{ list }}</div>
</template>

<style scoped></style>
