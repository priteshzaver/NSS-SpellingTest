<script setup>
const props = defineProps(['word'])

const sayWord = () => {
  const utterance = new SpeechSynthesisUtterance(props.word)
  return speechSynthesis.speak(utterance)
}
</script>

<template>
  <button @click="sayWord()">Say Word</button>
</template>

<style scoped></style>
