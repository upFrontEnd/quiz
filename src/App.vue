<template>
  <input type="text" v-model="page.title">
  Temps écoulé : {{ timer }}
</template>

<script setup>
import {ref, watch, watchEffect} from 'vue'
import { useTimer } from './composable/composable/useTimer'

const timer = useTimer()
const page = ref({
  title: ''
})

watchEffect(() => {
  document.title = page.value.title
})
</script>

