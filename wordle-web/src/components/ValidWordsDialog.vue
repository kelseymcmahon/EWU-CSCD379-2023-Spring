<template>
  <v-dialog v-model="dialog" width="650px">
    <template v-slot:activator="{ props }">
      <v-badge :content="validWordList.length" v-if="validWordList.length > 0">
        <v-btn color="primary" v-bind="props"> Hints </v-btn>
      </v-badge>
    </template>
    <v-card>
      <v-card-item>
        <v-card-title> Valid Words </v-card-title>
      </v-card-item>
      <v-card-text>
        <v-chip
          link
          color="primary"
          variant="flat"
          v-for="(word, i) in validWordList"
          :key="i"
          class="ma-1"
          @click="setWord(word)"
        >
          {{ word }}
        </v-chip>
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn color="primary" variant="flat" @click="dialog = false">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import { WordsService } from '@/scripts/wordsService'

const props = defineProps<{
  guess?: string
}>()

const emits = defineEmits<{
  (event: 'wordHintClicked', value: string): void
}>()

const validWordList = ref<Array<string>>([])
const dialog = ref(false)

watch(
  () => props.guess,
  () => {
    getValidWords()
  }
)

function getValidWords() {
  if (props.guess) {
    validWordList.value = WordsService.validWords(props.guess)
  }
}

function setWord(word: string) {
  emits('wordHintClicked', word)
  dialog.value = false
}
</script>
