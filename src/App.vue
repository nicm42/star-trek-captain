<script setup>
import { ref } from 'vue'
import Question from './components/Question.vue'
import questions from '../questions.json'

// Captains chosen with their counts
const captainCount = ref({})

captainCount.value = {
  TOS: 0,
  TNG: 0,
  DS9: 0,
  VOY: 0,
  ENT: 0,
  SNW: 0
}

// Keep track of which question we're on
const questionCount = ref(0)

function updateQuestionCount() {
  questionCount.value += 1
}

function updateCaptainCount(captainArray) {
  // Loop through the captainCount object
  // if it's in the captainArray, then update the value
  Object.keys(captainCount.value).forEach((item) => {
    if (captainArray.includes(item)) {
      captainCount.value[item] += 1
    }
  })
  console.log(captainCount.value)
}
</script>

<template>
  <h1>Which Star Trek Captain Are You?</h1>
  <p>Answer the questions to find out</p>
  <div v-for="(question, index) in questions" :key="question">
    <Question
      v-show="index === questionCount"
      :="question"
      :qnumber="index"
      :lastq="index === Object.keys(questions).length - 1"
      @questioncountupdate="updateQuestionCount"
      @captaincountupdate="updateCaptainCount"
    />
  </div>
</template>

<style scoped></style>
