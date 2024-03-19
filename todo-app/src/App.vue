<script setup>
import CompositionAPI from "@/views/CompositionAPI.vue";
import OptionsAPI from "@/views/OptionsAPI.vue";
</script>

<template>
  <div class="app">
    <div>
      <h1>Composition API</h1>
      <CompositionAPI/>
    </div>
    <div>
      <h1>Options API</h1>
      <OptionsAPI/>
    </div>
  </div>
</template>


<style scoped >
h1 {
  text-align: center;
}

.app {
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  gap: 20px;
  justify-content: center;
  align-items: center;
}

.app > div {
  border: 1px solid #000;
  padding: 20px;
  height: 50vh;
  border-radius: 5px;
  overflow: auto;
}
</style>
