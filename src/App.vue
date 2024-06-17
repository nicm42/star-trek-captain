<script setup>
import { ref } from 'vue'
import Question from './components/Question.vue'
import questions from '../questions.json'

// Randomise the order of the questions
const randomQuestions = questions
  .map((value) => ({ value, sort: Math.random() }))
  .sort((a, b) => a.sort - b.sort)
  .map(({ value }) => value)

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

function getWinnerImage() {
  // Find name of relevant image - which is just the surname with no capitals
  const winnerArr = winner.value.split(' ')
  const winnerImageName = winnerArr[winnerArr.length - 1].toLowerCase()
  return `./captains/${winnerImageName}.jpg`
}
</script>

<template>
  <h1>Which Star Trek Captain Are You?</h1>
  <p class="subtitle" v-show="!winner">Answer the questions to find out</p>
  <div class="questions-container">
    <div class="questions" v-for="(question, index) in randomQuestions" :key="question">
      <Transition>
        <Question
          v-show="index === questionCount"
          :class="{ showing: index === questionCount }"
          :="question"
          :qnumber="index"
          :lastq="index === Object.keys(questions).length - 1"
          @questioncountupdate="updateQuestionCount"
          @captaincountupdate="updateCaptainCount"
        />
      </Transition>
    </div>
    <Transition>
      <div v-if="winner" class="winner">
        <p>You are {{ winner }}</p>
        <img :src="getWinnerImage()" :alt="winner" />
      </div>
    </Transition>
  </div>
</template>

<style scoped>
h1 {
  font-size: 3.2rem;
  line-height: 1.1;
  text-align: center;
}

.subtitle {
  font-size: 2rem;
  text-align: center;
}

.questions-container {
  display: grid;
}

.questions,
.winner {
  grid-column: 1;
  grid-row: 1;
}

/* Vue transition */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.winner {
  font-size: 2rem;
  text-align: center;
}

.winner img {
  max-height: 200px;
  width: auto;
  object-fit: cover;
}
</style>
