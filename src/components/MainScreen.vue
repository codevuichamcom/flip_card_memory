<template>
  <h1>Pokemon Memories</h1>
  <p>Select mode to start game</p>
  <button @click="onChooseMode(16)">
    <span>4x4</span>
    <span>Easy</span>
  </button>
  <button @click="onChooseMode(36)">
    <span>6x6</span>
    <span>Normal</span>
  </button>
  <button @click="onChooseMode(64)">
    <span>8x8</span>
    <span>Hard</span>
  </button>
  <button @click="onChooseMode(100)">
    <span>10x10</span>
    <span>Supper Hard</span>
  </button>
  <copy-right />
</template>
<script>
import CopyRight from "./CopyRight.vue";
export default {
  methods: {
    onChooseMode(size) {
      this.$emit("onChooseMode", { size });
    },
  },
  components: {
    CopyRight,
  },
};
</script>
