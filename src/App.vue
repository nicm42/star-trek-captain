<script setup>
import Question from './components/Question.vue'
import questions from '../questions.json'
</script>

<template>
  <h1>Which Star Trek Captain Are You?</h1>
  <p>Answer the questions to find out</p>
  <Question :="questions[0]" />
</template>

<style scoped></style>
