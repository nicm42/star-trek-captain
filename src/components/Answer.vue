<script setup>
const props = defineProps({
  text: String,
  value: String,
  captain: Array
})

const emit = defineEmits(['captainupdate'])

function emitCaptain() {
  emit('captainupdate', props.captain)
}
</script>

<template>
  <div>
    <input
      type="radio"
      name="answer"
      :value="props.value"
      :id="props.value"
      :captain="props.captain"
      @input="emitCaptain"
    />
    <label :for="props.value">{{ props.text }}</label>
  </div>
</template>

<style scoped></style>
