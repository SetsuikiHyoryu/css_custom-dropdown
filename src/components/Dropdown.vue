<script setup lang="ts">
import { ref } from 'vue'

interface Props {
  list: string[]
}

interface Emits {
  (evnet: 'select-article', id: number): void
}

const props = defineProps<Props>()
const emits = defineEmits<Emits>()

const selectedValue = ref<string>('')
const isMenuDisplayed = ref<boolean>(false)

const select = (index: number): void => {
  selectedValue.value = props.list[index] ?? '--請選擇一篇文章--'
  emits('select-article', index + 1)
}

const controlMenu = (event: Event): void => {
  const target = event.target as HTMLElement

  // 如果菜單已打開則執行失焦
  if (isMenuDisplayed.value) {
    target.blur()
    return
  }

  // 如果菜單未打開則打開菜單（即僅標記菜單已打開）
  isMenuDisplayed.value = true
}
</script>

<template>
  <div id="dropdown" class="dropdown">
    <input
      type="text"
      class="dropdown-button"
      :value="selectedValue"
      @click="controlMenu"
      @blur="() => (isMenuDisplayed = false)"
      readonly
    />

    <div class="menu">
      <div class="placeholder" @click="() => select(-1)">
        --請選擇一篇文章--
      </div>

      <div
        class="item"
        v-for="(item, index) in list"
        :key="index"
        @click="() => select(index)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<style>
.dropdown {
  position: fixed;
  height: 2rem;
  top: 1.5rem;
  left: 1rem;
  width: 10rem;
}

.dropdown-button {
  box-sizing: border-box;
  cursor: pointer;
  height: 100%;
  padding: 0 1.5rem 0 0.7rem;
  width: 100%;
}

.dropdown::before {
  border: 0.3rem solid transparent;
  border-top: 0.5rem solid #333;
  content: '';
  display: block;
  position: absolute;
  right: 1rem;
  top: 40%;
  transition: top 300ms ease-in-out, transform 300ms ease-in-out;
}

.dropdown:focus-within::before {
  transform: rotate(180deg);
  top: 20%;
}

.menu {
  background: #fefefe;
  border-radius: 0.5rem;
  box-shadow: 0 0.5rem 1rem 0 rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
  left: 0;
  margin: 1rem 0 0;
  opacity: 0;
  padding: 0.3rem 0.3rem;
  pointer-events: none;
  position: absolute;
  top: 100%;
  transform: translateY(-1rem);
  transition: opacity 150ms ease-in-out, transform 150ms ease-in-out;
  width: 100%;
}

.menu:active,
.dropdown-button:focus + .menu {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}

.placeholder,
.item {
  box-sizing: border-box;
  padding: 0 0.5rem;
  cursor: pointer;
}

.placeholder {
  background: #efefef;
}

.placeholder:hover,
.item:hover {
  background: gray;
  color: #fff;
}
</style>
