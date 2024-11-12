<template>
  <div class="poetry">
    <div class="poetry__title">你</div>
    <template v-for="(poetry, index) of poetryList">
      <Transition name="fade" mode="out-in">
        <PoetryBoard
          class="poetry-board"
          v-if="index <= currentIndex"
          :key="index"
          :textList="poetry"
          @typed="onTyped"
        >
        </PoetryBoard>
      </Transition>
    </template>
  </div>
</template>

<script setup lang="ts">
import { onMounted, provide, ref } from "vue"
import PoetryBoard from "./PoetryBoard.vue"

const currentIndex = ref(0)
const isTransition = ref(true)
const isPlayOver = ref(false)
provide("isPlayOver", isPlayOver)
const onTyped = () => {
  if (currentIndex.value >= poetryList.value.length - 1)
    return (isPlayOver.value = true)
  isTransition.value = false
  setTimeout(() => {
    isTransition.value = true
  }, 500)

  currentIndex.value++

  console.log("触发事件")
}

const poetryList = ref([
  ["猪爸爸"],
  ["一辈子不长,别让人生输给了心态。", "人生,其实是一场自己跟自己的博弈,", "很多事情尽心尽力就好。"],
  ["凡事乐观以对,就没有越不过去的高山,", "善待自己,不要盲目较劲。"],
  ["我永远是你最坚强的后盾。"],
  ["相信自己,你值得最好的,", "我们一家三口一起加油,"],
  ["把所有好运都给你,", "愿你时来运转,风生水起……"],
  ["若无执念挂心头,人生何处不清欢"]
])

onMounted(() => {})
</script>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.poetry {
  line-height: 2;
  width: 400px;
  font-size: 16px;
  color: rgb(255, 136, 136);
  .poetry__title {
    font-size: 30px;
    font-weight: 600;
    color: rgb(255, 85, 85);
    margin-bottom: 30px;
  }
  .poetry-board {
    margin-top: 20px;
  }
}
</style>
