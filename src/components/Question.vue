<script setup>
import { ref } from 'vue'
import Answer from './Answer.vue'

const props = defineProps({
  question: String,
  answers: Array,
  qnumber: Number,
  lastq: Boolean
})

const emits = defineEmits(['captaincountupdate', 'questioncountupdate'])

const currentAnswer = ref()

const showQuestion = ref(true)

// For the answers, we have the text we want to display
// but we also need it to have no spaces or capitals
// for the ID and for the value
function createID(string) {
  return string.replace(/ /g, '-').toLowerCase()
}

function updateAnswer(val) {
  currentAnswer.value = val
}

function saveData() {
  // only do something if an answer has been selected
  if (currentAnswer.value) {
    // Update the captain count
    emits('captaincountupdate', currentAnswer.value)
    // Show the next question
    emits('questioncountupdate')
  }
}

function showCaptain() {
  saveData()
  // hide question if an answer has been selected
  if (currentAnswer.value) {
    showQuestion.value = false
  }
}
</script>

<template>
  <form v-show="showQuestion">
    <p>{{ props.qnumber + 1 }}. {{ props.question }}</p>
    <div class="answers">
      <Answer
        v-for="answer in props.answers"
        :key="answer.response"
        :text="answer.response"
        :value="createID(answer.response)"
        :captain="answer.captain"
        @captainupdate="updateAnswer"
      />
    </div>
    <button type="submit" v-show="!lastq" @click.prevent="saveData">Next</button>
    <button type="submit" v-show="lastq" @click.prevent="showCaptain">Submit</button>
  </form>
</template>

<style scoped>
/* Make sure the current question is at the top */
.showing {
  position: relative;
  z-index: 99;
}

.answers {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.5rem;
}

button {
  margin-top: 1rem;
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #213547;
  background-color: var(--starfleet-blue);
  cursor: pointer;
  transition: background-color 0.25s;
}
button:hover {
  background-color: var(--starfleet-blue-hover);
}
button:focus,
button:focus-visible {
  background-color: var(--starfleet-blue-hover);
  outline: 4px auto -webkit-focus-ring-color;
}
</style>
