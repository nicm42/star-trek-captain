<script setup>
/* import { ref } from 'vue' */
import Answer from './Answer.vue'

defineProps({
  msg: String
})

/* const count = ref(0) */
</script>

<template>
  <!--<h1>{{ msg }}</h1>-->

  <form>
    <p>Question goes here</p>
    <Answer />
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
