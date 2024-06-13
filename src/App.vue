<script setup>
import { ref } from 'vue'
import Question from './components/Question.vue'
import questions from '../questions.json'

// Captains chosen with their counts
const captainCount = ref({})

captainCount.value = {
  'James T Kirk': 0,
  'Jean-Luc Picard': 0,
  'Benjamin Sisko': 0,
  'Kathryn Janeway': 0,
  'Jonathan Archer': 0,
  'Christopher Pike': 0
}

// Keep track of which question we're on
const questionCount = ref(0)

function updateQuestionCount() {
  questionCount.value += 1
}

const winner = ref()

function updateCaptainCount(captainArray) {
  // Loop through the captainCount object
  // if it's in the captainArray, then update the value
  Object.keys(captainCount.value).forEach((item) => {
    if (captainArray.includes(item)) {
      captainCount.value[item] += 1
    }
  })
  // If that was the last question, calculate which captain has the most answers
  // if there's more than one winner then it'll choose whichever it finds last
  // (because it's looking at a ref, it can change order)
  if (questionCount.value == Object.keys(questions).length - 1) {
    console.log(captainCount.value)
    winner.value = Object.keys(captainCount.value).reduce((a, b) =>
      captainCount.value[a] > captainCount.value[b] ? a : b
    )
  }
}
</script>

<template>
  <h1>Which Star Trek Captain Are You?</h1>
  <p v-show="!winner">Answer the questions to find out</p>
  <!-- TODO show the questions in a random order -->
  <div class="questions" v-for="(question, index) in questions" :key="question">
    <Transition>
      <Question
        v-show="index === questionCount"
        :="question"
        :qnumber="index"
        :lastq="index === Object.keys(questions).length - 1"
        @questioncountupdate="updateQuestionCount"
        @captaincountupdate="updateCaptainCount"
      />
    </Transition>
  </div>
  <Transition>
    <p v-show="winner">You are {{ winner }}</p>
  </Transition>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.questions {
  position: relative;
}
</style>
