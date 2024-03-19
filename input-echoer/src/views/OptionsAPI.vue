<script>
export default {
  name: "OptionsAPI",
  data() {
    return {
      text: "",
    };
  }
}
</script>

<template>
  <input type="text" v-model="text">
  <p>{{ text }}</p>
</template>
