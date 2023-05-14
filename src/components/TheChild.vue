<script setup lang="ts">
import { reactive, ref, watch } from 'vue'
import type { ToBeWatched } from "@/interfaces/ToBeWatched";

const props = defineProps<{
  reftowatch: number[]
  reactivetowatch: ToBeWatched
}>()
const refTest1 = ref<number[]>(props.reftowatch)
const refTest2 = ref<number[]>(props.reftowatch)
const refTest3 = ref<number[]>(props.reftowatch)
const reactiveTest1 = reactive<{ arrayOfInterest: number[] }>(props.reactivetowatch)
const reactiveTest2 = reactive<{ arrayOfInterest: number[] }>(props.reactivetowatch)
const reactiveTest3 = reactive<{ arrayOfInterest: number[] }>(props.reactivetowatch)

watch(props.reftowatch, (newValue) => {
  refTest1.value = newValue
})

watch([props.reftowatch], ([newValue]) => {
  refTest2.value = newValue
})

watch(
  () => props.reftowatch,
  (newValue) => {
    refTest3.value = newValue
  }
)

watch(props.reactivetowatch, (newValue) => {
  reactiveTest1.arrayOfInterest = newValue.arrayOfInterest
})

watch([props.reactivetowatch], ([newValue]) => {
  reactiveTest2.arrayOfInterest = newValue.arrayOfInterest
})

watch(
  () => props.reactivetowatch,
  (newValue) => {
    reactiveTest3.arrayOfInterest = newValue.arrayOfInterest
  }
)
</script>

<template>
  <div class="child-grey">
    Ref of the array <i>a</i> watched directly: {{ refTest1 }}
  </div>
  <div class="child-grey">
    Ref of the array <i>a</i> watched through an array of sources: {{ refTest2 }}
  </div>
  <div class="child-grey">
    Ref of the array <i>a</i> watched through a getter: {{ refTest3 }}
  </div>
  <div class="child-grey">
    Reactive <i>b</i> watched directly: {{ reactiveTest1 }}
  </div>
  <div class="child-grey">
    Reactive <i>b</i> watched through an array of sources: {{ reactiveTest2 }}
  </div>
  <div class="child-grey">
    Reactive <i>b</i> watched through a getter: {{ reactiveTest3 }}
  </div>
</template>