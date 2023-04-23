<template>
  <v-sheet :color="props.color" class="letter-button d-flex">
    <div class="font-weight-bold text-uppercase text-h4 ma-auto">
      {{ props.char }}
    </div>
  </v-sheet>
</template>

<script setup lang="ts">
export interface Props {
  char?: string
  color?: string
}

const props = withDefaults(defineProps<Props>(), {
  char: '?',
  color: 'grey'
})
</script>
<style>
.letter-button {
  width: 50px;
  height: 50px;
  cursor: pointer;
}
</style>
