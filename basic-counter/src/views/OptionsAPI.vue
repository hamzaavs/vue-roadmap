<script>
export default {
  name: "OptionsAPI",
  data() {
    return {
      count: 0
    }
  }
}
</script>

<template>
  <div>
    <button @click="count--">-</button>
    <p>{{ count }}</p>
    <button @click="count++">+</button>
  </div>
</template>

<style scoped>
div {
  height: 100vh;
  display: flex;
  flex-direction: row;
  gap: 10px;
  justify-content: center;
  align-items: center;
}

button {
  height: 3rem;
  width: 3rem;
}

p {
  font-size: 2rem;
}
</style>

