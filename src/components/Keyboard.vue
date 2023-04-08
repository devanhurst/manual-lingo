<script setup>
import KeyboardKey from "./KeyboardKey.vue";

const props = defineProps(["guesses"]);
</script>

<template>
  <div class="keyboard">
    <div class="keyboard-row">
      <KeyboardKey :guesses="guesses" keyCode="81" label="Q" />
      <KeyboardKey :guesses="guesses" keyCode="87" label="W" />
      <KeyboardKey :guesses="guesses" keyCode="69" label="E" />
      <KeyboardKey :guesses="guesses" keyCode="82" label="R" />
      <KeyboardKey :guesses="guesses" keyCode="84" label="T" />
      <KeyboardKey :guesses="guesses" keyCode="89" label="Y" />
      <KeyboardKey :guesses="guesses" keyCode="85" label="U" />
      <KeyboardKey :guesses="guesses" keyCode="73" label="I" />
      <KeyboardKey :guesses="guesses" keyCode="79" label="O" />
      <KeyboardKey :guesses="guesses" keyCode="80" label="P" />
    </div>
    <div class="keyboard-row">
      <KeyboardKey :guesses="guesses" keyCode="65" label="A" />
      <KeyboardKey :guesses="guesses" keyCode="83" label="S" />
      <KeyboardKey :guesses="guesses" keyCode="68" label="D" />
      <KeyboardKey :guesses="guesses" keyCode="70" label="F" />
      <KeyboardKey :guesses="guesses" keyCode="71" label="G" />
      <KeyboardKey :guesses="guesses" keyCode="72" label="H" />
      <KeyboardKey :guesses="guesses" keyCode="74" label="J" />
      <KeyboardKey :guesses="guesses" keyCode="75" label="K" />
      <KeyboardKey :guesses="guesses" keyCode="76" label="L" />
    </div>
    <div class="keyboard-row">
      <KeyboardKey :guesses="guesses" keyCode="90" label="Z" />
      <KeyboardKey :guesses="guesses" keyCode="88" label="X" />
      <KeyboardKey :guesses="guesses" keyCode="67" label="C" />
      <KeyboardKey :guesses="guesses" keyCode="86" label="V" />
      <KeyboardKey :guesses="guesses" keyCode="66" label="B" />
      <KeyboardKey :guesses="guesses" keyCode="78" label="N" />
      <KeyboardKey :guesses="guesses" keyCode="77" label="M" />
    </div>
    <div class="keyboard-row controls">
      <KeyboardKey keyCode="187" label="Correct [+]" type="success" />
      <KeyboardKey keyCode="189" label="Almost [-]" type="warning" />
      <KeyboardKey keyCode="32" label="Incorrect [Space]" type="error" />
    </div>
    <div class="keyboard-row controls">
      <KeyboardKey keyCode="27" label="Reset [ESC]" type="default" />
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
