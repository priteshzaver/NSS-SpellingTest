<script setup>
import { computed } from 'vue'

const props = defineProps(['spellingWords'])

const correctCount = computed(() => {
  return props.spellingWords.filter((spellingWord) => {
    return spellingWord.word.toUpperCase() === spellingWord.userInput.toUpperCase()
  }).length
})

const hasPerfectScore = computed(() => {
  return correctCount.value === props.spellingWords.length
})
</script>

<template>
  <div>
    <div>
      <p>Results: {{ correctCount }} / {{ props.spellingWords.length }}</p>
      <p v-if="hasPerfectScore">PERFECT SCORE!</p>
    </div>
    <div v-for="spellingWord in spellingWords" :key="spellingWord.word">
      <span>You entered: {{ spellingWord.userInput }}</span>
      <span v-if="spellingWord.word.toUpperCase() === spellingWord.userInput.toUpperCase()"
        >Checkmark</span
      >
      <span v-else> X-mark </span>
      <span>{{ spellingWord.word }}</span>
    </div>
  </div>
</template>

<style scoped></style>
