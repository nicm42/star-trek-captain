<script setup>
const props = defineProps({
  text: String,
  value: String,
  captain: Array
})

const emit = defineEmits(['captainupdate'])
</script>

<template>
  <input
    type="radio"
    name="answer"
    :value="props.value"
    :id="props.value"
    :captain="props.captain"
    @input="emit('captainupdate', props.captain)"
  />
  <label :for="props.value">{{ props.text }}</label>
</template>

<style scoped></style>
