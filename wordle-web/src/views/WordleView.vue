<template>
  <v-container>
    <v-row class="py-4">
      <v-spacer />
      <h1>Wordle Mind Bender</h1>
      <v-spacer />
    </v-row>

    <GameBoard :game="game" @letterClick="addChar" />

    <KeyBoard @letterClick="addChar" :guessedLetters="game.guessedLetters" />

    <v-row>
      <v-spacer />
      <v-col cols="auto">
        <v-btn @click="checkGuess" @keyup.enter="checkGuess"> Check </v-btn>
      </v-col>
      <v-col cols="auto">
        <ValidWordsDialog :guess="guess" @word-hint-clicked="setWord" />
      </v-col>
      <v-spacer />
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import { WordleGame } from '@/scripts/wordleGame'
import { ref, reactive, onMounted, onUnmounted } from 'vue'
import GameBoard from '../components/GameBoard.vue'
import KeyBoard from '../components/KeyBoard.vue'
import ValidWordsDialog from '../components/ValidWordsDialog.vue'
import type { Letter } from '@/scripts/letter'
import { Word } from '@/scripts/word'

const guess = ref('')
const game = reactive(new WordleGame())

onMounted(() => {
  window.addEventListener('keyup', keyPress)
})

onUnmounted(() => {
  window.removeEventListener('keyup', keyPress)
})

function checkGuess() {
  game.submitGuess()
  guess.value = ''
}

function addChar(letter: Letter) {
  game.guess.push(letter.char)
  guess.value += letter.char
}

function keyPress(event: KeyboardEvent) {
  console.log(event.key)
  if (event.key === 'Enter') {
    checkGuess()
  } else if (event.key === 'Backspace') {
    guess.value = guess.value.slice(0, -1)
    game.guess.pop()
  } else if (event.key.length === 1 && event.key !== ' ') {
    guess.value += event.key.toLowerCase()
    game.guess.push(event.key.toLowerCase())
  }
}

function setWord(word: string) {
  game.guess = new Word()
  guess.value = word
  for (var i = 0; i < word.length; i++) {
    game.guess.push(word[i])
  }
  const index = game.guesses.indexOf(game.guess)
  game.guesses[index] = game.guess
  console.log(word)
  console.log(game.guess)
  console.log(game.guesses[index])
}
</script>
