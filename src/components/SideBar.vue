<template>
  <section class="sidebar">
    <div class="item">
      <i class="bi bi-window" @click="openClose()"></i>
      <div class="changeMen" v-show="this.open">
        <input
          class="changeGlass blur"
          type="range"
          v-model="blurInput"
          max="30"
        />
        <input
          class="colorInput"
          type="color"
          v-model="rgbaColor"
          value="#e66465"
        />
        <input
          class="changeColorOpacity"
          deafult=""
          type="range"
          v-model="colorInput"
          max="999"
        />
      </div>

      <a
        href="https://github.com/oguzhanascier"
        target="_blank"
        rel="noopener noreferrer"
        ><i class="bi bi-github"> </i
      ></a>

      <i class="bi bi-linkedin"></i>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      blurInput: null,
      colorInput: null,
      open: false,
      rgbaColor: null,
    };
  },
  methods: {
    //sidebar toogle
    openClose() {
      this.open = !this.open;
      this.$emit("sideBar", this.open);
    },
  },
  //  blur & color send parent &
  watch: {
    blurInput() {
      this.$emit("range", this.blurInput);
    },
    colorInput() {
      this.$emit("rangeC", this.colorInput);
    },
    rgbaColor(value) {
      this.$emit("rgba", value);
    },
  },
};
</script>

<style scoped>
.sidebar {
  position: absolute;
  height: 300px;
  width: 100%;
}

.changeGlass {
  position: absolute;
  top: 25%;
  left: 103%;
  width: 100px;
  background-color: rgba(128, 0, 128, 0.276);
}

.changeColorOpacity {
  position: absolute;
  top: 10%;
  left: 103%;
  width: 100px;
  background-color: #dcc58f;
}
.colorInput {
  position: absolute;
  top: 40%;
  left: 103%;
  width: 40px;
  height: 40;
}



@media only screen and (max-width: 768px) {
  .changeGlass {
  position: absolute;
  top: 80%;
  left: 93%;
  width: 100px;
  background-color: rgba(128, 0, 128, 0.276);
  transform: rotate(-90deg);

}

.changeColorOpacity {
  position: absolute;
  top: 80%;
  left: 103%;
  width: 100px;
  background-color: #dcc58f;
  transform: rotate(-90deg);

}
.colorInput {
  position: absolute;
  top: 10%;
  left: 97%;
  width: 40px;
  height: 40;
  transform: rotate(-90deg);
  z-index: 1;
}
.changeMen{

z-index: 1;
  
}


}
</style>
