<script setup>
import { computed, ref } from 'vue'
import spellingData from './spellingData'
import SpeechUtterance from './components/SpeechUtterance.vue'
import SpellingScore from './components/SpellingScore.vue'

const spellingWords = ref([...spellingData])
const currentIndex = ref(0)
const userAnswer = ref('')

const handleSubmit = () => {
  const activeWord = spellingWords.value[currentIndex.value]
  activeWord.userInput = userAnswer.value
  currentIndex.value++
  userAnswer.value = ''
}

const testFinished = computed(() => {
  return currentIndex.value >= spellingWords.value.length
})
</script>

<template>
  <div>
    <h1>Spelling Test</h1>
    <div v-if="!testFinished">
      <div>Word {{ currentIndex + 1 }} of {{ spellingWords.length }}</div>
      <SpeechUtterance :word="spellingWords[currentIndex].word" />
      <form @submit.prevent="handleSubmit">
        <input v-model="userAnswer" type="text" spellcheck="false" />
        <button>Submit</button>
      </form>
    </div>
    <div v-else>
      <SpellingScore v-if="testFinished" :spellingWords="spellingWords" />
    </div>
  </div>
</template>

<style scoped></style>
