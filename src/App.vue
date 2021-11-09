<template>
  <main-screen v-if="route === 'main'" @onChooseMode="onBeforeStart($event)" />
  <interact-screen
    :cardNumbers="cardNumbers"
    v-if="route === 'interact'"
    @onFished="showResult"
  />
  <result-screen v-if="this.route == 'result'" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data() {
    return {
      route: "main",
      cardNumbers: [],
    };
  },
  methods: {
    onBeforeStart(config) {
      const size = config.size;
      let count = 0;
      for (let i = 0; i < size; i++) {
        count++;
        this.cardNumbers.push({ value: count, isFlipped: false });
        if (count === size / 2) {
          count = 0;
        }
      }
      this.cardNumbers.sort(() => Math.random() - 0.5);
      this.route = "interact";
    },
    showResult() {
      this.route = "result";
    },
  },
};
</script>
