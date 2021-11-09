<template>
  <div class="card" @click="onToggleFlip()">
    <div class="card__inner" :class="{ 'is-flipped': isFlipped }">
      {{ card }}
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url('${require('@/assets/' + imageBack)}')`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: { card: { type: Number }, imageBack: { type: String } },
  data() {
    return {
      isFlipped: false,
      isDisable: false,
    };
  },
  methods: {
    onToggleFlip() {
      if (this.isFlipped && this.isDisable) {
        return;
      }
      this.isFlipped = !this.isFlipped;
      this.$emit("isFlip", this.isFlipped);
    },
    setDisable(isDisable) {
      this.isDisable = isDisable;
    },
  },
};
</script>
<style scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  height: 200px;
  perspective: 250px;
  /* width: 90px; */
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card.disabled .card__inner {
  cursor: default;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 18px 3px rgba(0, 0, 0, 0.2);
}
.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 60px 60px;
  height: 100%;
  width: 100%;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card__face--back .card__content {
  background-position: center center;
  background-repeat: no-repeat;
  background-size: contain;
  height: 100%;
  width: 100%;
}
</style>
