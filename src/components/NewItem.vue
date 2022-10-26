<template>
  <div>
    <div class="text-area" :class="{ toggle: !isBoard }">
      <i class="fa-solid fa-x" @click="close"></i>
      <div>
        <input
          type="text"
          class="title"
          v-model="title"
          placeholder="Keyword.."
        />

        <textarea
          class="area"
          placeholder="What are you think..?"
          v-model="textInput"
        ></textarea>
        <button class="run" @click="setText">Go</button>
      </div>
    </div>

    <div class="write" :class="{ toggle: isBoard }">
      <p>{{ text }}</p>
      <i class="bi bi-pen" @click="changeBoard"></i>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isBoard: false,
      textInput: "",
      text: "",
      title: "",
    };
  },
  methods: {
    changeBoard() {
      this.isBoard = !this.isBoard;
    },

    setText() {
      let date = new Date();
      let day = date.getDate();
      let month = date.getMonth()+1;
      let year = date.getFullYear();

      console.log(day,month,year)

      let randomNumber = "azFazQwwg" + Math.floor(Math.random() * 100 + "eQ5");
      this.$emit("reData", {
        id: randomNumber,
        title: this.title,
        date: { day, month, year },
        text: this.textInput,
        isCompleted: false,
      });

      this.textInput = "";
    },

    close() {
      this.isBoard = !this.isBoard;
    },
  },
};
</script>

<style scoped>
.toggle {
  display: none;
}

.run {
  display: block;
  position: absolute;
  right: 12%;
  width: 300px;
  height: 40px;
  border: none;
  background: rgba(255, 255, 255, 0.082);
  backdrop-filter: blur(0.5rem);
  border-radius: 10px;
  box-shadow: 0mm 0mm 1mm white;
  color: white;
  transition: 0.3s ease-in-out;
}

.run:hover {
  background: rgba(255, 255, 255, 0.482);
  color: rgba(0, 0, 0, 0.53);
}

.fa-solid {
  display: block;
  position: absolute;
  right: 7%;
  cursor: pointer;
  color: #ffffff9b;
}

.title {
  display: block;
  position: absolute;
  width: 300px;
  padding: 10px;
  right: 13%;
  bottom: 97%;
  background: rgba(255, 255, 255, 0.082);
  backdrop-filter: blur(1rem);
  box-shadow: 0mm 0mm 1mm white;
  border: none;
  border-radius: 10px;
}
</style>
