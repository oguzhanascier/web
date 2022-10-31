<template>
  <section class="sidebar">
    <div class="item">
      <i class="bi bi-window" @click="openClose()"></i>
      <div v-show="this.open">
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

      <div class="customCard" v-if="open">
        <p>backdrop-filter: blur({{ blurInput }}px)</p>
        <p>color: {{ rgbaColor }}</p>
        <p>opacity: 0.{{ colorInput }}</p>
      </div>
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
    openClose() {
      this.open = !this.open;
      console.log(this.open);
    },
    // colorChange(e){
    //   console.log(e.target.value)
    // }
  },
  computed: {
    // colorChange(e){
    //   // console.log(e)
    // }
  },
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
  position: relative;
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

.customCard {
  position: absolute;
  height: 120px;
  width: 200px;
  top: 65%;
  left: 5%;
  background: rgba(255, 255, 255, 0.094);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}
</style>
