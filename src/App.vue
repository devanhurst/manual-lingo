<script setup>
import { ref } from "vue";
import { NButton } from "naive-ui";

const currentLetter = ref(1);

const moveToNextLetter = () => {
  if (currentLetter.value < 26) {
    currentLetter.value++;
  }
  focusOnCurrentLetter();
};

const moveToPreviousLetter = () => {
  if (currentLetter.value > 1) {
    currentLetter.value--;
  }
  focusOnCurrentLetter();
};

const moveToLetterAbove = () => {
  if (currentLetter.value > 5) {
    currentLetter.value -= 5;
  }
  focusOnCurrentLetter();
};

const moveToLetterBelow = () => {
  if (currentLetter.value < 21) {
    currentLetter.value += 5;
  }
  focusOnCurrentLetter();
};

const moveToBeginningOfRow = () => {
  currentLetter.value = Math.floor((currentLetter.value - 1) / 5) * 5 + 1;
  focusOnCurrentLetter();
};

const focusOnCurrentLetter = () => {
  const currentLetterInput = document.getElementById(
    `letter-${currentLetter.value}`
  );
  currentLetterInput.select();
};

const handleClick = (event) => {
  currentLetter.value = event.target.id.split("-")[1];
};

const isAlphabetic = (key) => {
  return /^[a-zA-Z]$/.test(key);
};

const markAsCorrect = () => {
  const currentLetterInput = document.getElementById(
    `letter-${currentLetter.value}`
  );
  currentLetterInput.classList.remove("almost");
  currentLetterInput.classList.add("correct");

  moveToNextLetter();
};

const markAsAlmost = () => {
  const currentLetterInput = document.getElementById(
    `letter-${currentLetter.value}`
  );
  currentLetterInput.classList.remove("correct");
  currentLetterInput.classList.add("almost");

  moveToNextLetter();
};

const markAsNothing = () => {
  const currentLetterInput = document.getElementById(
    `letter-${currentLetter.value}`
  );

  currentLetterInput.classList.remove("correct");
  currentLetterInput.classList.remove("almost");

  moveToNextLetter();
};

const handleKeydown = (event) => {
  event.preventDefault();

  const keyCode = event.keyCode;
  const key = event.key;
  console.log(keyCode);

  if (isAlphabetic(key)) {
    event.target.value = event.key.toUpperCase();
    if (currentLetter.value % 5 === 0) {
      moveToBeginningOfRow();
    } else {
      moveToNextLetter();
    }
    return;
  }

  // Backspace
  if (keyCode === 8) {
    event.target.value = "";

    const currentLetterInput = document.getElementById(
      `letter-${currentLetter.value}`
    );
    currentLetterInput.classList.remove("correct");
    currentLetterInput.classList.remove("almost");

    moveToPreviousLetter();
    return;
  }

  // Mark as correct and move when pressing +=
  if (keyCode === 187) {
    markAsCorrect();
  }

  // Mark as correct/incorrect when  -_
  if (keyCode === 189) {
    markAsAlmost();
  }

  if (keyCode === 32) {
    markAsNothing();
  }

  if (keyCode === 39) {
    moveToNextLetter();
  }

  if (keyCode === 37) {
    moveToPreviousLetter();
  }

  if (keyCode === 38) {
    moveToLetterAbove();
  }

  if (keyCode === 40) {
    moveToLetterBelow();
  }
};

setTimeout(() => {
  focusOnCurrentLetter();
}, 200);
</script>

<template>
  <main>
    <div class="grid">
      <input
        v-for="i in 25"
        :id="`letter-${i}`"
        maxlength="1"
        @keydown="handleKeydown"
        @click="handleClick"
        class="letter"
      />
    </div>

    <n-button class="button" type="success" @click="markAsCorrect"
      >Correct Letter, Correct Position [+]</n-button
    >
    <n-button class="button" type="warning" @click="markAsAlmost"
      >Correct Letter, Incorrect Position [-]</n-button
    >
    <n-button class="button" type="info" @click="markAsNothing"
      >Incorrect Letter [Space]</n-button
    >
  </main>
</template>

<style scoped>
main {
  margin: auto;
  width: 50%;
}

.grid {
  display: grid;
  grid-template-columns: repeat(5, 20%);
  grid-template-rows: repeat(5, 20%);
  margin-bottom: 10px;
}
.letter {
  font-size: 4rem;
  text-align: center;
  border: 3px solid black;
  color: black;
}

.letter.correct {
  background-color: #18a058;
  color: white;
}

.letter.almost {
  background-color: #f0a020;
  color: white;
}

.letter.nothing {
  background-color: #2080f0;
  color: white;
}
.button {
  width: 100%;
  margin-bottom: 5px;
}
</style>
