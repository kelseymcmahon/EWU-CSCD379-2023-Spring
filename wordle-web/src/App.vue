<template>
  <!-- <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink> | <RouterLink to="/wordle">Wordle</RouterLink> |
        <RouterLink to="/about">About</RouterLink>
      </nav>
      <v-btn @click="setInverseTheme"> Inverse Theme </v-btn>
      <v-btn @click="setDarkTheme"> Dark Theme </v-btn>
    </div>
  </header>

  <RouterView /> -->
  <v-app id="vue-app">
    <v-app-bar color="primary" density="compact" :elevation="2">
      <template v-slot:prepend>
        <v-app-bar-nav-icon density="comfortable" @click="drawer = !drawer" />
      </template>
      <v-icon class="ml-2" icon="mdi mdi-unicorn-variant" />
      <v-app-bar-title class="ml-1">
        <span class="font-weight-bold text-uppercase"> Magic Games </span>
      </v-app-bar-title>
      <template v-slot:append>
        <v-menu :close-on-content-click="false" location="bottom">
          <template v-slot:activator="{ props }">
            <v-btn icon density="comfortable" v-bind="props">
              <v-icon icon="mdi-dots-vertical" />
            </v-btn>
          </template>
          <v-card min-width="300">
            <v-card-item>
              <v-card-title> Settings </v-card-title>
            </v-card-item>
            <v-divider />
            <v-card-text>
              <v-btn-toggle v-model="currentTheme" rounded="0" color="primary" group>
                <v-btn value="Light" @click="setInverseTheme">
                  <v-icon icon="mdi-weather-sunny" start /> Light
                </v-btn>
                <v-btn value="Dark" @click="setDarkTheme">
                  <v-icon icon="mdi-weather-night" start />Dark
                </v-btn>
              </v-btn-toggle>
            </v-card-text>
          </v-card>
        </v-menu>
      </template>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" location="left" temporary>
      <v-list :items="items"></v-list>
    </v-navigation-drawer>
  </v-app>
</template>

<script setup lang="ts">
import { useTheme } from 'vuetify/lib/framework.mjs'
import { ref } from 'vue'

const theme = useTheme()
const currentTheme = ref('Dark')
const drawer = ref(false)
const items = [
  {
    title: 'Home',
    value: 'foo'
  },
  {
    title: 'Game',
    value: 'bar'
  },
  {
    title: 'Fizz',
    value: 'fizz'
  },
  {
    title: 'Buzz',
    value: 'buzz'
  }
]

getThemeName()

function getThemeName() {
  if (theme.global.name.value === 'inverse') {
    currentTheme.value = 'Light'
  }
  currentTheme.value = 'Dark'
}

function setInverseTheme() {
  theme.global.name.value = 'inverse'
}

function setDarkTheme() {
  theme.global.name.value = 'dark'
}
</script>
