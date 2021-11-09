<template>
  <h1>This is interact screen{{ size }}</h1>
  <div class="container">
    <card-fip
      :ref="`card-${index}`"
      :card="card"
      :imageBack="`images/${card.value}.png`"
      v-for="(card, index) in cardNumbers"
      :key="index"
      @click="onClick(index, cardNumbers)"
      @isFlip="setFlipped($event, index, cardNumbers)"
    />
  </div>
</template>

<script>
import CardFip from "./Card.vue";
export default {
  components: {
    CardFip,
  },
  props: {
    cardNumbers: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      old: -1,
      disable: [],
      count: 0,
    };
  },
  methods: {
    onClick(index, cardNumbers) {
      if (this.old !== -1) {
        if (index !== this.old) {
          let i1 = this.old;
          let i2 = index;
          if (cardNumbers[i1].value === cardNumbers[i2].value) {
            this.count += 2;
            setTimeout(() => {
              this.$refs["card-" + i1].setDisable(true);
              this.$refs["card-" + i2].setDisable(true);
            }, 800);
          } else {
            setTimeout(() => {
              this.$refs["card-" + i1].onToggleFlip();
              this.$refs["card-" + i2].onToggleFlip();
            }, 800);
          }
        }
        this.old = -1;
      } else {
        if (
          cardNumbers[index].isFlipped &&
          !this.disable[index] &&
          this.old == -1
        ) {
          this.old = index;
        }
      }
      if (this.count == this.cardNumbers.length) {
        setTimeout(() => {
          this.$emit("onFished");
        }, 800);
      }
    },
    setFlipped(isFlipped, index, cardNumbers) {
      cardNumbers[index].isFlipped = isFlipped;
    },
  },
};
</script>

<style scoped>
.container {
  display: grid;
  width: 1200px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}
</style>
