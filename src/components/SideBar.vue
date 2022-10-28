<template>
     <section class="sidebar">
      <div class="item">
        <i class="bi bi-window" @click="openClose()"></i>
        <div v-show="this.open">
          <input class="changeGlass" type="range" v-model="inputRange" >
        </div>   
        <a href="https://github.com/oguzhanascier"  target="_blank" rel="noopener noreferrer"><i class="bi bi-github"> </i></a>
        <i class="bi bi-linkedin"></i>
      </div>
    </section>
</template>

<script >
export default{
  data(){
    return{
      inputRange:0,
      open:false,
    }
  },
  methods:{
    openClose(){
      this.open=!this.open
      console.log(this.open)
    },
  }
}

</script>

<style scoped>
.sidebar{
  position: relative;
}
.changeGlass{
position: absolute;
top: 25%;
left: 103%;
width: 100px;
background-color: rgba(128, 0, 128, 0.276);
}

.changeGlass::-moz-range-thumb {
  background: #DCC58F;
  cursor: pointer;
}
</style>