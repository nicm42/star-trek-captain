<script setup>
const props = defineProps({
  text: String,
  value: String
})
</script>

<template>
  <input type="radio" name="answer" :value="props.value" :id="props.value" />
  <label :for="props.value">{{ props.text }}</label>
</template>

<style scoped></style>
