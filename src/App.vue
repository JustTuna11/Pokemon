<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @ChooseModeGame="OnHandleBeforeStart($event)"
  />
  <interract-srceen
    v-if="statusMatch === 'inMatch'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-srceen
    v-if="statusMatch === 'Complete'"
    :finishTime="finishTime"
    @onReplay="onReplay"
  ></result-srceen>
</template>

<script>
import MainScreen from "./components/MainSrceen.vue";
import InterractSrceen from "./components/InteractSrceen.vue";
//import { shuffled } from "./utils/array";
import ResultSrceen from "./components/ResultSrceen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InterractSrceen,
    ResultSrceen,
  },
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlock: 0, // Tổng số thẻ trong các màn với mỗi lần click
        cardsContext: [], // Mảng chứa các giá trị của các thẻ bài (Dược merge từ 2 mảng có cùng giá trị và số lượng phần tử với nhau)
        startedAt: null,
      },
      finishTime: 0,
    };
  },
  methods: {
    OnHandleBeforeStart(config) {
      console.log(config);
      this.settings.totalOfBlock = config.totalOfBlock;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const card = [...firstCards, ...secondCards];

      //this.settings.cardsContext = shuffled(shuffled(card));
      this.settings.cardsContext = card;
      //console.log(this.settings.cardsContext);
      this.settings.startedAt = new Date().getTime();
      //console.log(this.settings.startedAt);
      this.statusMatch = "inMatch";
    },
    onGetResult() {
      // Lấy thời gian hoàn thành
      this.finishTime = new Date().getTime() - this.settings.startedAt;

      // Chuyển màn
      this.statusMatch = "Complete";
    },
    onReplay() {
      this.statusMatch = "default";
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: var(--dark);
  color: var(--light);
  z-index: 2;
  top: 0;
  left: 0;
}
</style>
