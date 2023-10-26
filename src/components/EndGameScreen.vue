<template>
  <div class="end-game w-50 mx-auto mt-5 pt-5">
    <h1 class="display-1 text-white fw-bold d-flex justify-content-center">
      ✨ Congratulations ✨
    </h1>
    <p class="text-white fs-1 d-flex justify-content-center mb-0">
      Bạn mất {{ timePlay }} giây để hoàn thành.
    </p>
    <p class="text-white fs-1 d-flex justify-content-center">
      {{
        timePlay >= 50
          ? "Quá gà"
          : timePlay >= 40
          ? "Cũng tạm được"
          : timePlay >= 30
          ? "Ghê taaa"
          : "Pro quá mannn"
      }}
    </p>
    <button
      @click="playAgain()"
      class="play-again d-block px-4 py-2 mx-auto rounded-2 fs-5"
    >
      Cày lại
    </button>
  </div>
</template>
<script>
export default {
  props: {
    timePlay: {
      type: [Number, String, Array, Object],
      required: true,
    },
  },
  methods: {
    playAgain() {
        this.$emit("onPlayAgain")
    }
  }
};
</script>
<style lang="css" scoped>
.play-again {
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  border: 2px solid white;
}
.play-again:hover {
  color: rgb(255, 255, 0);
  background-color: rgba(0, 0, 0, 0.5);
  border: 2px solid rgb(255, 255, 0);
}
</style>
