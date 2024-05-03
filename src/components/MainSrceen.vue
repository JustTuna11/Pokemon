<template>
  <div class="screen">
    <div class="screen_inner">
      <h1>POKE MEMORIES</h1>
      <h3>Select Mode To Start</h3>
      <div class="action">
        <button @click="ChooseModeGame(16)">
          <p>4x4</p>
          <p>Easy</p>
        </button>
        <button @click="ChooseModeGame(36)">
          <p>6x6</p>
          <p>Medium</p>
        </button>
        <button @click="ChooseModeGame(64)">
          <p>8x8</p>
          <p>Hard</p>
        </button>
        <button @click="ChooseModeGame(100)">
          <p>10x10</p>
          <p>Imposible</p>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    ChooseModeGame(totalOfBlock) {
      this.$emit("ChooseModeGame", { totalOfBlock });
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
.screen_inner {
  position: relative;
  top: 30%;
  left: 25%;
  width: 50%;
  font-size: 50px;
  text-align: center;
}
.action button {
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
  border: 1px white solid;
  background-color: var(--dark);
  color: white;
  width: 120px;
  height: 100px;
}
.action :hover {
  background-color: white;
  color: black;
  cursor: pointer;
}
.action p {
  font-size: 20px;
  font-family: "Odibee Sans";
}
</style>
