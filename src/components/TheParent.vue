<script setup lang="ts">
import TheChild from '@/components/TheChild.vue'
import { reactive, ref } from 'vue'
import type { ToBeWatched } from '@/interfaces/ToBeWatched'

const a = ref<number[]>([0])
const b = reactive<ToBeWatched>({ arrayOfInterest: [1] })

const randomlyChangeProps = () => {
  a.value = [getRandomInt(100)]
  b.arrayOfInterest = [getRandomInt(100)]
}

const getRandomInt = (max: number) => {
  return Math.floor(Math.random() * max);
}
</script>

<template>
  <div class="flex-column card">
    <button @click="randomlyChangeProps">Change props</button>
    <div>From parent: <i>a</i>={{ a }} and <i>b</i>={{ b }}</div>
    <TheChild :reftowatch="a" :reactivetowatch="b"></TheChild>
  </div>
</template>