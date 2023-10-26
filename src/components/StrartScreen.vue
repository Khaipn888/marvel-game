<template>
  <div class="main-screen w-50 mx-auto ">
    <p class="d-flex justify-content-center display-1 fw-bold mt-5 pt-5 text-white ">Avengers Memories</p>
    <p class="fs-1 fw-bold  d-flex justify-content-center text-white">Select mode to start game</p>
    <div class="d-flex justify-content-center ">
      <button class="game-mode" @click="onStart(16)">
        <p>4x4</p>
        <p>Bronze</p>
      </button>
      <button class="game-mode" @click="onStart(36)">
        <p>6x6</p>
        <p>Platinum</p>
      </button>
      <button class="game-mode" @click="onStart(64)">
        <p>8x8</p>
        <p>Master</p>
      </button>
      <button class="game-mode" @click="onStart(100)">
        <p>10x10</p>
        <p>Challenger</p>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: "StratSceen",
  methods: {
    onStart(totalOfCard) {
      this.$emit("onStart", {totalOfCard})
    }
  }

};
</script>
<style lang="css" scoped>
  .game-mode{
    border-radius: 10px;
    width: 140px;
    height: 140px;
    margin: 0px 5px;
    border: 3px solid black;
    background-color: rgba(255, 255, 255, 0.5);
  }
  .game-mode:hover{
    color: white;
    background: rgba(0, 0, 0, 0.5);
    border: 3px solid rgb(251, 255, 0);
  }
  .game-mode p{
    margin-bottom: 0;
    font-size: 2rem;
  }
</style>
