<script setup>
import { NButton } from "naive-ui";
import { computed } from "vue";
const props = defineProps(["keyCode", "label", "type", "guesses"]);

const handleClick = () => {
  document.dispatchEvent(
    new KeyboardEvent("keydown", { keyCode: props.keyCode, key: props.label })
  );
};

const keyIsGuessed = () => {
  return props.guesses.flat().some((letter) => {
    return letter.letter === props.label;
  });
};

const keyIsInCorrectPosition = () => {
  return props.guesses.flat().some((letter) => {
    return letter.letter === props.label && letter.correctPosition;
  });
};

const keyIsInWord = () => {
  return props.guesses.flat().some((letter) => {
    return letter.letter === props.label && letter.correctLetter;
  });
};

const type = computed(() => {
  if (!props.guesses) return null;

  if (keyIsInCorrectPosition()) {
    return "success";
  } else if (keyIsInWord()) {
    return "warning";
  } else if (keyIsGuessed()) {
    return "default";
  } else {
    return "info";
  }
});
</script>

<template>
  <n-button
    class="keyboard-key"
    :size="'small'"
    :type="type || props.type || 'default'"
    @click="handleClick"
    >{{ label }}</n-button
  >
</template>

<style scoped>
.keyboard-key {
  margin: 0 2px;
}
</style>
