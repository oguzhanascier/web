<template>
  <div>
    <div class="text-area" :class="{ toggle: !isBoard }">
      <i class="fa-solid fa-x" @click="close"></i>
      <div>
        <input
          type="text"
          class="title"
          v-model="title"
          placeholder="Keyword.. (at least 3 letters)"
          ref="inputFocus"
        />

        <textarea
          class="area"
          placeholder="What are you think..?"
          v-model="textInput"
        ></textarea>
        <div class="opt">
          <select class="min" v-model="minute">
            <option value="">Min</option>

            <option v-for="i in number" :key="i" clas>{{ i }}</option>
          </select>
          <select class="sec" v-model="second">
            <option value="">Sec</option>
            <option v-for="i in number" :key="i">{{ i }}</option>
          </select>
        </div>
        <button class="run" @click="setText" >Go</button>
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
      timer: false,
      number: [],
      textInput: "",
      text: "",
      title: "",
      second: 0,
      minute: 0,
      hour: 0,
    };
  },
  methods: {
    changeBoard() {
      this.isBoard = !this.isBoard;
      for (let i = 0; i <= 59; i++) {
        this.number.push(i);
      }
    },

    setText() {
      
      if(this.title.split("").length<3){
        this.$refs.inputFocus.focus()
      }else{
        let date = new Date();
      let day = date.getDate();
      let month = date.getMonth() + 1;
      let year = date.getFullYear();


      let randomNumber = "azFazQwwg" + Math.floor(Math.random() * 100 + "eQ5");
      this.$emit("reData", {
        id: randomNumber,
        title: this.title,
        date: { day, month, year },
        text: this.textInput,
        isCompleted: false,
        second: 0,
        timerS: this.second,
        minute: 0,
        timerM: this.minute,
        hour: 0,
        timerH: 0,
        cardActive: false,

        cardComplete: false,
      });
      console.log(this.reData)


      }


      this.textInput = "";
      this.title=""
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

.opt {
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 10%;
  right: 95%;
}
select {
  background: rgba(128, 0, 128, 0.084);
  backdrop-filter: blur(1rem);
  border: none;
  border-top: 1px solid white;
  margin-bottom: 5px;
  border-radius: 5px;
}
</style>
