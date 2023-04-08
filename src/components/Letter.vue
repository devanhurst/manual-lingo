<script setup>
import { computed } from "vue";
const props = defineProps([
  "letter",
  "selected",
  "correctLetter",
  "correctPosition",
]);

const borderColor = computed(() => {
  if (props.selected) {
    return "#2080f0";
  }
  return "black";
});

const backgroundColor = computed(() => {
  if (props.correctPosition && props.correctLetter) {
    return "#18a058";
  } else if (props.correctLetter) {
    return "#f0a020";
  } else {
    return "white";
  }
});
</script>

<template>
  <div class="letter" :class="selected && 'selected'">{{ letter }}</div>
</template>

<style scoped>
.letter {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3rem;
  height: 4.5rem;
  width: 4.5rem;
  background-color: v-bind(backgroundColor);
  max-width: 5rem;
  border: 3px solid v-bind(borderColor);
  color: black;
}
</style>
