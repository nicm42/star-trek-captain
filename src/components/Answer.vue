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

<style scoped>
input {
  appearance: none;
  position: relative;
  padding-left: 1rem;
}

input::before,
input::after {
  content: '';
  position: absolute;
  border-radius: 50%;
  aspect-ratio: 1;
  cursor: pointer;
}

input::before {
  border: 1px solid #213547;
  width: 1rem;
  left: 0;
}

input::after {
  background-color: var(--starfleet-blue);
  width: 0.75rem;
  left: 50%;
  top: 50%;
  transform: translate(-44%, -60%);
  opacity: 0;
}

input:checked::after {
  opacity: 1;
}

label {
  cursor: pointer;
}
</style>
