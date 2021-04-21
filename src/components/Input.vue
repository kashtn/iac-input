<template>
  <div class="container">
    <div class="imgContainer" :class="{ focused: flag }">
      <img
        src="https://avatars.mds.yandex.net/get-zen_doc/28064/pub_5d559c90bc251400ad8cb3f3_5d564d3ba98a2a00ad2598a7/scale_600"
        alt="image"
      />
    </div>
    <div class="inputContainer">
      <h4 class="title" :class="{ focused: flag }">HUGH IS</h4>
      <div>
        <input
          class="input"
          type="text"
          v-model="hours"
          @input="checkInput"
          @focus="clicked"
          @blur="clicked"
          :style="{
            width: hours.length <= 6 ? '50px' : hours.length * 7 + 'px',
          }"
        />
        <span>hours old</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hours: "",
      flag: false,
    };
  },
  methods: {
    checkInput() {
      let cleanStr = this.hours.replace(/\s/g, "");
      if (cleanStr.length > 3) {
        let counter = 0;
        let arr = cleanStr.split("");
        for (let i = arr.length - 1; i >= 0; i -= 1) {
          counter += 1;
          if (counter === 3) {
            arr.splice(i, 0, " ");
            counter = 0;
          }
        }
        this.hours = arr.join("");
      }
    },
    clicked() {
      this.flag = !this.flag;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
}
.imgContainer {
  display: flex;
  align-items: center;
  margin-right: 10px;
  border-radius: 50%;
  border: 1px solid transparent;
  &.focused {
    border: 1px solid blue;
  }
  img {
    border-radius: 50%;
    width: 80px;
    height: 80px;
  }
}
.inputContainer {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  .title {
    margin: 0;
    margin-bottom: 20px;
  }
}
.input {
  border: none;
  border-bottom: 1px solid rgba(204, 204, 204, 0.763);
  width: 50px;
  margin-right: 10px;
  &:focus {
    outline: none;
    border-bottom-color: blue;
  }
}
</style>
