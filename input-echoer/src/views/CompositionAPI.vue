<script setup>
import {ref} from "vue";

const text = ref("")
</script>

<template>
  <input type="text" v-model="text">
  <p>{{ text }}</p>
</template>
