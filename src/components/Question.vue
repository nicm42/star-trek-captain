<script setup>
/* import { ref } from 'vue' */
import Answer from './Answer.vue'

const props = defineProps({
  question: String,
  answers: Array
})

// For the answers, we have the text we want to display
// but we also need it to have no spaces or capitals
// for the ID and for the value
function createID(string) {
  return string.replace(/ /g, '-').toLowerCase()
}

/* const count = ref(0) */
</script>

<template>
  <!--<h1>{{ msg }}</h1>-->

  <form>
    <p>{{ props.question }}</p>
    <Answer
      v-for="answer in props.answers"
      :key="answer"
      :text="answer"
      :value="createID(answer)"
    />
    <button type="submit">Next</button>
  </form>

  <!--
  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
  -->
</template>

<style scoped></style>
