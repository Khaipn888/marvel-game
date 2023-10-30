<template>
  <div
    class="frame-container mx-auto mt-4"
    :style="{
      width: `${
        (((Math.round(622 / Math.sqrt(cardArray.length)) - 16) * 4) / 3 + 16) *
        Math.sqrt(cardArray.length)
      }px`,
    }"
  >
    <Card
      v-for="(card, index) in cardArray"
      :key="index"
      :ref="`card-${index}`"
      :urlImage="`${card}.jpg`"
      :cardValue="{ index, value: card }"
      @onHandleFlipp="checkRules($event)"
      :numOfCard="cardArray.length"
      :disableClick="disableClick"
    />
  </div>
</template>
<script>
import Card from "./Card.vue";
export default {
  props: {
    cardArray: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    Card,
  },
  data() {
    return {
      correctPair: 0,
      cardChosing: [],
      disableClick: false
    };
  },
  methods: {
    checkRules(card) {
      if (this.cardChosing.length === 2) return false;
      this.cardChosing.push(card);
      console.log(this.cardChosing.length);
      if(this.cardChosing.length === 2) {
        this.disableClick = true;
        setTimeout(() => {
        this.disableClick = false;     
        }, 1000);
      }
      if (
        this.cardChosing.length === 2 &&
        this.cardChosing[0].value === this.cardChosing[1].value
      ) {
        // truong hop dung
        console.log("đúng");
        this.correctPair++;
        this.$refs[`card-${this.cardChosing[0].index}`][0].setDisableTrue();
        this.$refs[`card-${this.cardChosing[1].index}`][0].setDisableTrue();
        this.cardChosing = [];
        if (this.correctPair * 2 == this.cardArray.length) {
          setTimeout(() => {
            this.$emit("onEndGame");
          }, 800);
        }
      } else if (
        this.cardChosing.length === 2 &&
        this.cardChosing[0].value !== this.cardChosing[1].value
      ) {
        // truong hop sai
        console.log("sai");
        const cardChosingCopy = [...this.cardChosing];
        this.cardChosing = [];
        setTimeout(() => {
          this.$refs[`card-${cardChosingCopy[0].index}`][0].onCloseCard();
          this.$refs[`card-${cardChosingCopy[1].index}`][0].onCloseCard();
          setTimeout(() => {
            this.$refs[`card-${cardChosingCopy[0].index}`][0].setDisableFalse();
            this.$refs[`card-${cardChosingCopy[1].index}`][0].setDisableFalse();
          }, 500);
        }, 800);
      } else return false;
    },
  },
};
</script>
<style lang="css" scoped></style>
