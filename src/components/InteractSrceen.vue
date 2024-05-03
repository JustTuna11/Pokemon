<template>
  <div
    class="screen"
    :style="{
      height: `${
        ((920 - 16 * 2) / Math.sqrt(this.cardsContext.length)) *
          Math.sqrt(this.cardsContext.length) +
        16 * Math.sqrt(this.cardsContext.length)
      }px`,
    }"
  >
    <div
      class="screen_inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(this.cardsContext.length)) * 3) / 4 +
            16) *
          Math.sqrt(this.cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index: index, value: card }"
        @flipCart="checkRule($event)"
        :cardsContext="cardsContext"
      />
    </div>
  </div>
</template>
<script>
import CardFlip from "./CardPoke.vue";
export default {
  components: {
    CardFlip,
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      rules: [],
      // mảng này dùng để nhận id của 2 ảnh khi chúng ta chơi.
      //Nếu 2 ảnh đó trùng thì card đó sẽ lật mãi, còn nếu mà 2 ảnh đó không trùng thì tự động lật lại
    };
  },
  methods: {
    checkRule(numberCard) {
      //console.log(numberCard);
      if (this.rules.length === 2) return false;
      this.rules.push(numberCard);
      // console.log(this.rules);
      // console.log(this.$refs[`card-${this.rules[0].index}`]);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("OK");
        // Thêm class disable_card vào component cardPoke
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisable();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisable();
        this.rules = [];

        // Điều kiện để kết thúc game đấu là tất cả thẻ đều được lật
        //const arr = [];
        const disableElements = document.querySelectorAll(
          ".screen .card.disable"
        );
        //arr.push(disableElements);
        // console.log(document.querySelectorAll("disableElements"));
        // disableElements.forEach((element) => {
        //   const computedStyle = window.getComputedStyle(element);
        //   const pointer = computedStyle.getPropertyValue("pointer");
        //   console.log(pointer);
        //   arr.push(pointer);
        // });
        console.log(disableElements.length);
        if (disableElements.length === this.cardsContext.length - 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 1000);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        //console.log(this.$refs[`card-${this.rules[0].index}`]);
        // đóng 2 thẻ nếu 2 thẻ đó khác nhau
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          // refresh lại
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>
<style lang="css" scoped>
.screen .screen_inner {
  display: flex;
  flex-wrap: wrap;
  margin: auto;
  position: relative;
  margin: 16px auto;
}
</style>
