<template>
  <div
    class="card-mv"
    :class="{ disable: isDisableClick }"
    :style="{
      width: `${((Math.round(622 / Math.sqrt(numOfCard)) - 16) * 4) / 3}px`,
      height: `${Math.round(610 / Math.sqrt(numOfCard)) - 16}px`,
    }"
  >
    <div
      class="card-mv__inner"
      :class="{ 'card-mv-flipped': isFlipped }"
      @click="handleFlipp()"
    >
      <div class="card-mv__face card-mv__face--front">
        <div class="card-mv__content"></div>
      </div>
      <div class="card-mv__face card-mv__face--back">
        <div
          class="card-mv__content"
          :style="{ backgroundImage: `url(${returnUrlImage(urlImage)})` }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    urlImage: {
      type: String,
      required: true,
    },
    cardValue: {
      type: [Number, String, Array, Object],
      required: true,
    },
    numOfCard: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisableClick: false,
    };
  },
  methods: {
    handleFlipp() {
      if (this.isDisableClick) return false;
      this.isFlipped = !this.isFlipped;
      this.isDisableClick = true;
      if (this.isFlipped) {
        this.$emit("onHandleFlipp", this.cardValue);
      }
    },
    onCloseCard() {
      this.isFlipped = false;
      console.log("close card");
    },
    setDisableTrue() {
      this.isDisableClick = true;
    },
    setDisableFalse() {
      this.isDisableClick = false;
    },
    returnUrlImage(image) {
      return new URL("/src/assets/images/" + image, import.meta.url).href;
    },
  },
};
</script>
<style lang="css" scoped>
.card-mv {
  display: inline-block;
  margin: 0.3rem 0.5rem;
}
.disable .card-mv__inner {
  cursor: default;
}
.card-mv__inner {
  border: none;
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card-mv__inner.card-mv-flipped {
  transform: rotateX(-180deg);
}
.card-mv__face {
  position: absolute;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.5);
  height: 100%;
  width: 100%;
}

.card-mv__face--front .card-mv__content {
  background: rgba(255, 255, 255, 0.8) url("../assets/images/f.png") no-repeat
    center center;
  background-size: 50%;
  width: 100%;
  height: 100%;
}
.card-mv__face--back {
  background-color: gray;
  transform: rotateX(-180deg);
}
.card-mv__face--back .card-mv__content {
  width: 100%;
  height: 100%;
  background-size: 100% 100%;
}
</style>
