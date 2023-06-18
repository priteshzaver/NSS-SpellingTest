<script setup>
import { ref } from 'vue'
import spellingData from './spellingData'
import SpeechUtterance from './components/SpeechUtterance.vue'

const spellingWords = ref([...spellingData])
const currentIndex = ref(0)
const userAnswer = ref('')

const handleSubmit = () => {
  const activeWord = spellingWords.value[currentIndex.value]
  activeWord.userInput = userAnswer.value
  currentIndex.value++
  userAnswer.value = ''
}
</script>

<template>
  <h1>Spelling Test</h1>
  <div>
    <SpeechUtterance :word="spellingWords[currentIndex].word" />
  </div>
  <form @submit.prevent="handleSubmit">
    <input v-model="userAnswer" type="text" spellcheck="false" />
    <button>Submit</button>
  </form>
</template>

<style scoped></style>
