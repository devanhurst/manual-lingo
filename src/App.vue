<script setup>
import { ref } from "vue";
import { NConfigProvider, darkTheme } from "naive-ui";
import Keyboard from "./components/Keyboard.vue";
import Letter from "./components/Letter.vue";

const currentGuessIndex = ref(0);
const currentLetterIndex = ref(0);
const wordLength = 5;

const emptyGuess = {
  correctLetter: false,
  correctPosition: false,
  value: "",
};

const generateNewGuess = () => new Array(wordLength).fill({ ...emptyGuess });

const guesses = ref([generateNewGuess()]);

const moveToNextLetter = () => {
  if (currentLetterIndex.value < wordLength - 1) {
    currentLetterIndex.value++;
  }
};

const moveToPreviousLetter = () => {
  if (currentLetterIndex.value > 0) {
    currentLetterIndex.value--;
  }
};

const moveToPreviousGuess = () => {
  if (currentGuessIndex.value > 0) {
    currentGuessIndex.value -= 1;
  }
};

const moveToNextGuess = () => {
  if (currentGuessIndex.value === guesses.value.length - 1) {
    guesses.value.push(generateNewGuess());
  }

  if (currentGuessIndex.value < guesses.value.length - 1) {
    currentGuessIndex.value += 1;
  }
};

const moveToBeginningOfRow = () => {
  currentLetterIndex.value = 0;
};

const isAlphabetic = (key) => {
  return /^[a-zA-Z]$/.test(key);
};

const markAsCorrect = () => {
  const existingGuess =
    guesses.value[currentGuessIndex.value][currentLetterIndex.value];
  guesses.value[currentGuessIndex.value][currentLetterIndex.value] = {
    ...existingGuess,
    correctLetter: true,
    correctPosition: true,
  };

  if (currentLetterIndex.value === wordLength - 1) {
    moveToNextGuess();
    moveToBeginningOfRow();
  } else {
    moveToNextLetter();
  }
};

const markAsAlmost = () => {
  const existingGuess =
    guesses.value[currentGuessIndex.value][currentLetterIndex.value];
  guesses.value[currentGuessIndex.value][currentLetterIndex.value] = {
    ...existingGuess,
    correctLetter: true,
    correctPosition: false,
  };

  if (currentLetterIndex.value === wordLength - 1) {
    moveToNextGuess();
    moveToBeginningOfRow();
  } else {
    moveToNextLetter();
  }
};

const markAsNothing = () => {
  const existingGuess =
    guesses.value[currentGuessIndex.value][currentLetterIndex.value];
  guesses.value[currentGuessIndex.value][currentLetterIndex.value] = {
    ...existingGuess,
    correctLetter: false,
    correctPosition: false,
  };

  if (currentLetterIndex.value === wordLength - 1) {
    moveToNextGuess();
    moveToBeginningOfRow();
  } else {
    moveToNextLetter();
  }
};

const setLetter = (letter) => {
  const existingGuess =
    guesses.value[currentGuessIndex.value][currentLetterIndex.value];
  guesses.value[currentGuessIndex.value][currentLetterIndex.value] = {
    ...existingGuess,
    letter: letter.toUpperCase(),
  };
};

const resetGame = () => {
  guesses.value = [generateNewGuess()];

  currentGuessIndex.value = 0;
  currentLetterIndex.value = 0;
};

const handleKeydown = (event) => {
  event.preventDefault();

  const code = event.code;
  const key = event.key;

  if (isAlphabetic(key)) {
    setLetter(key);

    if (currentLetterIndex.value === wordLength - 1) {
      moveToBeginningOfRow();
    } else {
      moveToNextLetter();
    }
    return;
  }

  switch (code) {
    case "Backspace": {
      guesses.value[currentGuessIndex.value][currentLetterIndex.value] = {
        correctLetter: false,
        correctPosition: false,
        letter: "",
      };

      moveToPreviousLetter();
      break;
    }

    case "Digit1": {
      markAsCorrect();
      break;
    }

    case "Digit2": {
      markAsAlmost();
      break;
    }

    case "Digit3": {
      markAsNothing();
      break;
    }

    case "ArrowLeft": {
      moveToPreviousLetter();
      break;
    }

    case "ArrowUp": {
      moveToPreviousGuess();
      break;
    }

    case "Space":
    case "ArrowRight": {
      moveToNextLetter();
      break;
    }

    case "ArrowDown": {
      moveToNextGuess();
      break;
    }

    case "Escape": {
      resetGame();
      break;
    }
  }
};

const handleClick = (guessIndex, letterIndex) => {
  currentGuessIndex.value = guessIndex;
  currentLetterIndex.value = letterIndex;
};

setTimeout(() => {
  document.addEventListener("keydown", handleKeydown);
}, 100);
</script>

<template>
  <n-config-provider :theme="darkTheme">
    <main>
      <div class="game-wrapper">
        <div class="grid">
          <div class="guess" v-for="(guess, guessIndex) in guesses">
            <Letter
              v-for="(letter, letterIndex) in guess"
              :letter="letter.letter"
              @click="handleClick(guessIndex, letterIndex)"
              :correctPosition="letter.correctPosition"
              :correctLetter="letter.correctLetter"
              :selected="
                currentGuessIndex === guessIndex &&
                currentLetterIndex === letterIndex
              "
            />
          </div>
        </div>

        <Keyboard :guesses="guesses" />
      </div>
    </main>
  </n-config-provider>
</template>

<style scoped>
main {
  display: flex;
  justify-content: end;
  align-items: end;
  flex-direction: column;
  height: 100svh;
  padding-bottom: 20px;
}

.game-wrapper {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.grid {
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
  flex: 1;
  justify-content: end;
}

.guess {
  display: flex;
  justify-content: center;
  flex-direction: row;
}

.button {
  width: 100%;
  margin-bottom: 5px;
}
</style>
