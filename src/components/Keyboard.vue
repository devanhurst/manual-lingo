<script setup>
import KeyboardKey from "./KeyboardKey.vue";

const props = defineProps(["guesses"]);
</script>

<template>
  <div class="keyboard">
    <div class="keyboard-row">
      <KeyboardKey :guesses="guesses" code="KeyQ" label="Q" />
      <KeyboardKey :guesses="guesses" code="KeyW" label="W" />
      <KeyboardKey :guesses="guesses" code="KeyE" label="E" />
      <KeyboardKey :guesses="guesses" code="KeyR" label="R" />
      <KeyboardKey :guesses="guesses" code="KeyT" label="T" />
      <KeyboardKey :guesses="guesses" code="KeyY" label="Y" />
      <KeyboardKey :guesses="guesses" code="KeyU" label="U" />
      <KeyboardKey :guesses="guesses" code="KeyI" label="I" />
      <KeyboardKey :guesses="guesses" code="KeyO" label="O" />
      <KeyboardKey :guesses="guesses" code="KeyP" label="P" />
    </div>
    <div class="keyboard-row">
      <KeyboardKey :guesses="guesses" code="KeyA" label="A" />
      <KeyboardKey :guesses="guesses" code="KeyS" label="S" />
      <KeyboardKey :guesses="guesses" code="KeyD" label="D" />
      <KeyboardKey :guesses="guesses" code="KeyF" label="F" />
      <KeyboardKey :guesses="guesses" code="KeyG" label="G" />
      <KeyboardKey :guesses="guesses" code="KeyH" label="H" />
      <KeyboardKey :guesses="guesses" code="KeyJ" label="J" />
      <KeyboardKey :guesses="guesses" code="KeyK" label="K" />
      <KeyboardKey :guesses="guesses" code="KeyL" label="L" />
    </div>
    <div class="keyboard-row">
      <KeyboardKey :guesses="guesses" code="KeyZ" label="Z" />
      <KeyboardKey :guesses="guesses" code="KeyX" label="X" />
      <KeyboardKey :guesses="guesses" code="KeyC" label="C" />
      <KeyboardKey :guesses="guesses" code="KeyV" label="V" />
      <KeyboardKey :guesses="guesses" code="KeyB" label="B" />
      <KeyboardKey :guesses="guesses" code="KeyN" label="N" />
      <KeyboardKey :guesses="guesses" code="KeyM" label="M" />
      <KeyboardKey code="8" label="«" type="error" />
    </div>
    <div class="keyboard-row controls">
      <KeyboardKey code="Digit1" label="Correct [1]" type="success" />
      <KeyboardKey code="Digit2" label="Almost [2]" type="warning" />
      <KeyboardKey code="Digit3" label="Incorrect [3]" type="error" />
    </div>
    <div class="keyboard-row controls">
      <KeyboardKey code="Escape" label="Reset [ESC]" type="default" />
    </div>
  </div>
</template>

<style scoped>
.keyboard-row {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 4px;
}

.keyboard-row.controls {
  margin-top: 10px;
}
</style>
