<template>
  <div class="">
    <StrartScreen
      v-if="screenStatus === 'default'"
      @onStart="handleChangeInGameScreen($event)"
    />
    <InGameScreen
      v-if="screenStatus === 'ingame'"
      :cardArray="settings.cardArray"
      @onEndGame="handleChangeEndGameScreen()"
    />
    <EndGameScreen
      v-if="screenStatus === 'endgame'"
      :timePlay="settings.timePlay"
      @onPlayAgain=" () => { this.screenStatus = 'default' }"
    />
  </div>
</template>
<script>
import StrartScreen from "./components/StrartScreen.vue";
import InGameScreen from "./components/InGameScreen.vue";
import EndGameScreen from "./components/EndGameScreen.vue";
import { shuffled } from "./utils/Merge";

export default {
  name: "App",
  components: {
    StrartScreen,
    InGameScreen,
    EndGameScreen,
  },
  data() {
    return {
      settings: {
        totalOfCard: 0,
        cardArray: [],
        startTime: null,
        timePlay: null,
      },
      screenStatus: "default",
    };
  },
  methods: {
    handleChangeInGameScreen(gameMode) {
      this.settings.totalOfCard = gameMode.totalOfCard;
      const arr = Array.from(
        { length: gameMode.totalOfCard / 2 },
        (_, i) => i + 1
      );
      const cards = [...arr, ...arr];
      this.settings.cardArray = shuffled(
        shuffled(shuffled(shuffled(shuffled(cards))))
      );
      this.settings.startTime = new Date().getTime();
      this.screenStatus = "ingame";
    },
    handleChangeEndGameScreen() {
      this.screenStatus = "endgame";
      this.settings.timePlay = Math.round(
        (new Date().getTime() - this.settings.startTime) / 1000
      );
      console.log("time play: " + this.settings.timePlay);
    },
  },
};
</script>
<style lang="css" scoped></style>
