<template>
  <div class="container">
    <div class="row d-flex justify-content-around">
      <div
        class="col-lg-4 col-md-6 col-sm-12"
        v-for="(item, index) in setData"
        :key="index"
      >
        <div class="card" :class="{ cardComplete: item.cardComplete }">
          <div class="card-body scrollText">
            <h5 class="card-title">{{ item.title }}</h5>
            <h6 class="card-subtitle mb-2 text-muted">
              {{ item.date.day }}.{{ item.date.month }}.{{ item.date.year }}
            </h6>
            <p class="card-text">
              {{ item.text }}
            </p>
          </div>

          <div class="timer" :class="{ completeTimer: item.cardActive }">
            <i
              class="bi bi-alarm"
              @click="timerStart(item)"
              v-show="!item.cardActive"
            ></i>

            <span style="margin-left: 15px" v-if="item.hour < 10"
              >0{{ item.hour }}:</span
            >
            <span style="margin-left: 15px" v-else>{{ item.hour }}:</span>

            <span v-if="item.minute < 10">0{{ item.minute }}:</span>
            <span v-else>{{ item.minute }}:</span>

            <span v-if="item.second < 10">0{{ item.second }}</span>
            <span v-else>{{ item.second }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { setTransitionHooks } from "@vue/runtime-core";
import NewItem from "./NewItem.vue";
export default {
  props: ["setData"],
  components: {
    NewItem,
  },
  data() {
    return {
      clock: null,
      second: 3,
      minute: 0,
    };
  },
  methods: {
    timerStart(item) {
      console.log(item.second);


      item.cardActive = true //clock icon open/close

      if (item.cardActive === true) {
        let time = item;

        let interval=setInterval(() => {
          time.second++;
          if (time.second >= 60) {
            time.minute += 1;
            time.second = 0;
          }
          if (time.minute >= 60) {
            time.hour += 1;
            time.minute = 0;
          }
          if (time.second == time.timerS && time.minute == time.timerM) {
            alert(item.title);
            item.cardActive = false;
            item.cardComplete=true
          clearInterval(interval)

          }
        }, 1000);
      }
      //******************************************************** */

      console.log(this.cardActive);

      // setInterval(() => {
      //   let now = new Date();
      // let second = now.getSeconds();
      // let minute = now.getMinutes();
      // let hour = now.getHours();

      //   let timsec = Math.abs(sec - second);
      //   let timmit = Math.abs(min - minute);
      //   let timhou = Math.abs(hou - hour);

      //   item.second = timsec;
      //   item.minute = timmit;
      //   item.hour = timhou;
      // }, 1000);
    },
  },
  watch: {
    timerStart(value) {
      console.log(value);
    },
  },
};
</script>

<style scoped>
.card-title {
  font-weight: 700;
  margin-bottom: 20px;
}
.timer {
  display: flex;
  align-items: center;
}

.pl-pa {
  margin-left: 15px;
}

.pl-pa button {
  border: none;
  box-shadow: 0mm 0mm 2mm rgba(255, 255, 255, 0.587);
  border-top: 1px solid rgba(255, 255, 255, 0.585);
  border-right: 1px solid rgba(255, 255, 255, 0.427);
  border-radius: 5px;

  background: rgba(255, 255, 255, 0.369);
  color: rgba(128, 0, 128, 0.495);
  transition: 0.5s ease;
}

.pl-pa button:hover {
  box-shadow: 0mm 0mm 6mm rgba(255, 255, 255, 1);
  color: rgba(128, 0, 128, 0.795);
}

.bi-alarm {
  color: #666;
  font-size: 24px;
  padding: 0;
  margin: 0;
  color: white;
  text-shadow: 0mm 0mm 2mm black;
  cursor: pointer;
}
.scrollText {
  font-size: medium;
  overflow: auto;
  height: 100%;
  width: 100%;
}
/* width */
::-webkit-scrollbar {
  width: 4px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px rgba(128, 128, 128, 0.287);
  border-radius: 10px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgba(128, 18, 206, 0.403);
  border-radius: 10px;
}

.cardComplete {
  background: rgba(255, 0, 0, 0.03);
  backdrop-filter: blur(0.5rem);

  border: none;
  border-top: 3px solid rgba(180, 0, 240, 0.43);
  border-right: 1px solid rgba(180, 0, 240, 0.264);
  border-radius: 30px;

  height: 450px;
  width: 350px;

  margin: 1.3rem;
  padding: 1rem;

  color: white;
}

.completeTimer {
  color: red;
}

.active {
  display: none;
}
</style>
