<script setup>
const props = defineProps({
  text: String,
  value: String,
  captain: Array
})

const emit = defineEmits(['captainupdate'])
</script>

<template>
  <div class="answer-container">
    <input
      type="radio"
      name="answer"
      :value="props.value"
      :id="props.value"
      :captain="props.captain"
      @input="emit('captainupdate', props.captain)"
    />
    <label :for="props.value">{{ props.text }}</label>
  </div>
</template>

<style scoped>
.answer-container {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

input {
  cursor: pointer;
  width: 1.5rem;
  aspect-ratio: 1;
  accent-color: var(----starfleet-blue);
}

label {
  cursor: pointer;
}

@media (prefers-color-scheme: light) {
  input::before {
    border: 1px solid #213547;
  }
}
</style>
