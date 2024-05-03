<template>
  <div class="screen">
    <div class="screen_inner">
      <h1>ùi dụ mẹ bạn đỉnh vll bạn ôiii</h1>
      <p>{{ Math.round(finishTime / 1000) }} seconds</p>
      <button class="action" @click="Replay">Chơi lại đi đừng ngại</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    finishTime: {
      type: Number,
      required: true,
    },
  },
  methods: {
    Replay() {
      console.log("asd");
      this.$emit("onReplay");
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
  font-family: "Odibee Sans";
}
.screen_inner {
  position: relative;
  top: 30%;
  left: 25%;
  width: 50%;
  font-size: 50px;
  text-align: center;
}
.action {
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
  border: 1px white solid;
  background-color: var(--dark);
  color: white;
  width: 200px;
  height: 100px;
  font-family: "Odibee Sans";
}
.screen_inner .action:hover {
  background-color: white;
  color: black;
  cursor: pointer;
}
.screen_inner .action {
  font-size: 24px;
}
</style>
