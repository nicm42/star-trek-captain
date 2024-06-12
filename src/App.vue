<script setup>
import { ref } from 'vue'
import Question from './components/Question.vue'
import questions from '../questions.json'

// Captains chosen with their counts
const captainCount = ref(0)

captainCount.value = {
  TOS: 0,
  TNG: 0,
  DS9: 0,
  VOY: 0,
  ENT: 0,
  SNW: 0
}

function updateCaptainCount(captainArray) {
  // Loop through the captainCount object
  // if it's in the captainArray, then update the value
  Object.keys(captainCount.value).forEach((item) => {
    if (captainArray.includes(item)) {
      captainCount.value[item] += 1
    }
  })
}
</script>

<template>
  <h1>Which Star Trek Captain Are You?</h1>
  <p>Answer the questions to find out</p>
  <Question :="questions[0]" @captaincountupdate="updateCaptainCount" />
</template>

<style scoped></style>
