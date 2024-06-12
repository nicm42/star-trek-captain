<script setup>
import { ref } from 'vue'
import Answer from './Answer.vue'

const props = defineProps({
  question: String,
  answers: Array
})

const emit = defineEmits(['captaincountupdate'])

const currentAnswer = ref(0)

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
  // Update the captain count
  emit('captaincountupdate', currentAnswer.value)
}
</script>

<template>
  <form>
    <p>{{ props.question }}</p>
    <Answer
      v-for="answer in props.answers"
      :key="answer.response"
      :text="answer.response"
      :value="createID(answer.response)"
      :captain="answer.captain"
      @captainupdate="updateAnswer"
    />
    <button type="submit" @click.prevent="saveData">Next</button>
  </form>
</template>

<style scoped></style>
