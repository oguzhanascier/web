<template>
  <div class="relative">
      <input
        type="text"
        v-model="searchInput"
        class="search"
        placeholder=" Search Keywords.."
      />

    <SideBar
      @range="blurV = $event"
      @rangeC="colorV = $event"
      @rgba="rgbaC = $event"
      @sideBar="isOpen = $event"
    ></SideBar>

    <div class="container">
      <div class="row d-flex justify-content-around">
        <!-- loop -->
        <div
          class="col-xxl-4 col-xl-4 col-lg-6 col-md-6 col-sm-8 col-xs-12"
          v-for="(item, index) in filteredPosts"
          :key="index"
        >
          <!--##############-->
          <div
            class="card"
            :class="{ cardComplete: item.cardComplete }"
            :style="customStyle"
            v-if="!isOpen"
          >
            <div class="card-body scrollText">
              <span class="trashSpan"
                ><i class="fa-solid fa-trash" @click="deleteItem(index)"></i
              ></span>

              <h5 class="card-title">{{ item.title }}</h5>

              <h6 class="card-subtitle mb-2 text-muted">
                {{ item.date.day }}.{{ item.date.month }}.{{ item.date.year }}
              </h6>
              <p class="card-text">
                {{ item.text }}
              </p>
            </div>

            <div
              class="timer"
              :class="{ completeTimer: item.cardActive }"
              v-if="(!item.timerM == 0) | (!item.timerS == 0)"
            >
              <i
                class="bi bi-alarm"
                @click="timerStart(item, index)"
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
              <span
                class="stopWatch ms-2 text"
                @click="stopWatch(item)"
                v-show="item.cardActive"
                ><i class="fa-solid fa-pause"></i
              ></span>
            </div>
          </div>
          <div class="card customCard" :style="customStyle" v-if="isOpen">
          {{ customStyle }}
        </div>
        </div>
        
      </div>
      <div class="row">
        <div class="col-6" v-for="i in completeItem" :key="i">
          <p>{{ i.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NewItem from "./NewItem.vue";
import SideBar from "./SideBar.vue";
export default {
  props: ["setData"],
  components: {
    NewItem,
    SideBar,
  },
  data() {
    return {
      searchInput: "",
      clock: null,
      second: 0,
      minute: 0,
      interval: null,
      completeItem: [],
      blurV: "8",
      colorV: "30",
      rgbaC: "#00000008",
      isOpen: null,
      
    };
  },
  methods: {
    //setting watch
    timerStart(item, index) {
      item.cardActive = true; //clock icon open/close

      if (item.cardActive === true) {
        let time = item;

        this.interval = setInterval(() => {
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
            item.cardComplete = true;
            clearInterval(this.interval);
          }
        }, 1000);
      }
      localStorage.textItem = JSON.stringify(newNotes);
    },
    //stop watch
    stopWatch(item) {
      item.cardActive = false;
      clearInterval(this.interval);
    },
    // delete item
    deleteItem(index) {
      this.setData.splice(index, 1);
    },
  },

  computed: {
    // search
    filteredPosts() {
      let lowerValue = this.searchInput;
      return this.$props.setData.filter((item) =>
        item.title.toLowerCase().includes(lowerValue.toLowerCase())
      );
    },

    // card style
    customStyle() {
      let color = this.colorV.padStart(3, "0");

      console.log(this.blurV);

      return {
        "backdrop-filter": `blur(${this.blurV}px)`,

        "-webkit-backdrop-filter": `blur(${this.blurV}px)`,

        background:
          "rgba(" +
          parseInt(this.rgbaC.slice(-6, -4), 16) +
          "," +
          parseInt(this.rgbaC.slice(-4, -2), 16) +
          "," +
          parseInt(this.rgbaC.slice(-2), 16) +
          "," +
          "." +
          color +
          ")",

        // width: [this.blurV + "px"],
        // height: [this.blurV + "px"],
      };
    },
  },
};
</script>

<style scoped>
.card-title {
  font-weight: 700;
  margin-bottom: 20px;
}

.trashSpan {
  position: absolute;
  top: 4%;
  right: 6%;
  border-top: 1px solid white;
  border-radius: 5px;
  cursor: pointer;
}

.fa-trash {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(128, 0, 128, 0.341);
  color: rgb(255, 255, 255);

  width: 25px;
  height: 25px;
  border-radius: 5px;
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
  color: rgba(128, 0, 128, 0.529);
}

.active {
  display: none;
}

.stopWatch {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 25px;
  height: 25px;
  border-radius: 5px;
  background: rgba(128, 0, 128, 0.529);
  color: rgba(255, 255, 255, 0.985);
  cursor: pointer;
}

.search {
  display: block;
  position: fixed;
  top: 2%;
  left: 50%;
  transform: translate(-50%);
  width: 400px;
  z-index: 1;
  background-color: rgba(255, 255, 255, 0.444);
  backdrop-filter: blur(0.1rem);
  border-radius: 15px;
  border: none;
  filter: drop-shadow(0mm 0mm 1mm rgba(128, 0, 128, 0.555));
  padding: 5px 15px;
  outline: none;
  transition: 0.3s ease-in-out;
}

@media only screen and (max-width: 768px) {
  .relative {
    position: relative;
  }
  .search {
    position: absolute;
    top: 0%;
    left: 50%;
    width: 350px;
  }
 
}

.search:focus {
  filter: drop-shadow(0mm 0mm 1mm rgba(248, 167, 6, 0.555));
}

.blur {
  backdrop-filter: blur(9px);
}

.customCard {
  position: absolute;
  top: 45%;
  left: 45%;
  transform: translate(-50%, -50%);
}


</style>
