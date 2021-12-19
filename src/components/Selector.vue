<script setup lang="ts">
import { computed, ref } from 'vue'

interface Props {
  list: string[]
}

interface Emits {
  (event: 'selectArticle', id: number): void
}

const props = defineProps<Props>()
const emits = defineEmits<Emits>()

const placeholder = computed(() => {
  return selectedValue.value ? '' : '--請選擇一篇文章--'
})

const selectedValue = ref<string>('')
const isMenuDisplayed = ref<boolean>(false)

const select = (index: number): void => {
  selectedValue.value = props.list[index]
  emits('selectArticle', index + 1)
}

const controlMenu = (event: Event): void => {
  const target: HTMLElement = event.target as HTMLElement

  if (isMenuDisplayed.value) {
    target.blur()
    return
  }

  isMenuDisplayed.value = true
}
</script>

<template>
  <div class="dropdown">
    <input
      type="text"
      class="display-bar"
      :value="selectedValue"
      :placeholder="placeholder"
      @click="controlMenu"
      @blur="() => (isMenuDisplayed = false)"
      readonly
    />

    <div class="menu">
      <a class="placeholder" @click="() => select(-1)"> --請選擇一篇文章-- </a>

      <a
        class="item"
        v-for="(item, index) in list"
        @click="() => select(index)"
      >
        {{ item }}
      </a>
    </div>
  </div>
</template>

<style scoped>
.dropdown {
  position: fixed;
  top: 1rem;
  height: 2rem;
  width: 10rem;
}

.display-bar {
  align-items: center;
  border: 0.07rem solid #333;
  box-sizing: border-box;
  cursor: pointer;
  display: flex;
  padding: 0.3rem 0.5rem;
  width: 100%;
}

.menu {
  background: #fefefe;
  border-radius: 0.5rem;
  box-shadow: 0 0.5rem 0.5rem 0 rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
  left: 0;
  opacity: 0;
  padding: 0.5rem;
  position: absolute;
  pointer-events: none;
  top: calc(100% + 0.5rem);
  transform: translateY(-1rem);
  transition: opacity 150ms ease-in-out, transform 150ms ease-in-out;
  width: 100%;
}

.menu:active,
.display-bar:focus + .menu {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}

.placeholder {
  background: #efefef;
}

.placeholder,
.item {
  cursor: pointer;
  display: block;
  text-decoration: none;
}

.placeholder:hover,
.item:hover {
  background: gray;
  color: #fff;
}
</style>
