<template>
  <div
    class="card"
    :class="{ disable: isDisable }"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(this.cardsContext.length)}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(this.cardsContext.length)) * 3) / 4
      }px`,
    }"
  >
    <!-- :class="{ disable: true }" -->
    <div
      class="card_inner"
      :class="{ is_flipped: isFlipped == true }"
      @click="OnToggelFlipCard"
      :style="isDisable ? `cursor: default` : `cursor: pointer`"
    >
      <div class="card_face card_face_front">
        <div
          class="card_content"
          :style="{
            backgroundSize: `${
              (((920 - 16 * 4) / Math.sqrt(this.cardsContext.length)) * 3) /
              4 /
              3
            }px ${
              (((920 - 16 * 4) / Math.sqrt(this.cardsContext.length)) * 3) /
              4 /
              3
            }px`,
          }"
        ></div>
      </div>
      <div class="card_face card_face_back">
        <div
          class="card_content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      require: true,
    },
    card: {
      type: [String, Number, Object],
    },
    cardsContext: {
      type: Array,
      require: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisable: false,
    };
  },
  methods: {
    // Hàm lật thẻ
    OnToggelFlipCard() {
      if (this.isDisable === true) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped === true) {
        this.$emit("flipCart", this.card);
      }
      console.log((920 - 16 * 4) / Math.sqrt(this.cardsContext.length));
    },
    // Hàm tự động đóng thẻ lại
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onEnableDisable() {
      this.isDisable = true;
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 16px;
  margin-bottom: 16px;
}
.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 0.5s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card_inner.is_flipped {
  transform: rotateY(-180deg);
}
.card_face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card_face_front .card_content {
  /* background-color: red; */
  background: url("../assets/images/icon_back.png") no-repeat center;
  height: 100%;
  width: 100%;
}

.card_face_back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card_face_back .card_content {
  background-position: center center;
  background-size: contain;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
.card.disable {
}
</style>
