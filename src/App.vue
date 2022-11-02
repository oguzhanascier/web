<template>
  <div class="container-fluid">
    <Container :setData="textItem"></Container>
    <NewItem @reData="textItem.push($event)"></NewItem>
  </div>
</template>

<script>
import Container from "./components/Container.vue";
import NewItem from "./components/NewItem.vue";
export default {
  components: {
    Container,
    NewItem,
  },
  data() {
    return {
      textItem: [],
    };
  },

  mounted() {
    if (localStorage.textItem) {
      this.textItem = JSON.parse(localStorage.textItem);
    }
  },
  watch: {
    textItem(newNotes) {
      localStorage.textItem = JSON.stringify(newNotes);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  /* Importing a font from google fonts. */
  @import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;700&display=swap");
  font-family: "Open Sans", sans-serif;
  /* Setting the background image to the body of the page. */
  background: url(./assets/milad-fakurian-PGdW_bHDbpI-unsplash.jpg);
  background-position: center center;
  background-size: 100% 100%;
  background-attachment: fixed;
  background-repeat: no-repeat;
  min-height: 100vh;
  /* Centering the content of the page. */
  display: flex;
  justify-content: center;
  align-items: center;
  overflow-x: hidden;
  z-index: -9999;
}
.container-fluid {
  height: 100%;
  widows: 100%;
  position: relative;
}
.container {
  display: flex;
  position: relative;
  justify-content: center;
  width: 100%;
  min-height: 100vh !important;
  border-radius: 30px;
  margin-top: 3%;
  margin-bottom: 3%;
}

.card {
  background: #00000008;
  /* backdrop-filter: blur(8px) ; */
  margin: 1.5rem;
  padding: 1.3rem;
  margin-bottom: 1rem;
  width: 350px;
  height: 450px;
  top: 13%;
  left: 50%;
  transform: translate(-50%);
  border: none;
  border-top: 3px solid rgba(255, 255, 255, 0.936);
  border-right: 1px solid rgba(255, 255, 255, 0.664);
  border-radius: 30px;

  color: white;
}

/* @media only screen and (max-width: 576px) {
  .card {
    top: 18%;
    left: 50%;
    transform: translate(-60.5%);
    width: 300px;
    height: 350px;
    margin-bottom: 1rem;
  }
} */

/* @media only screen and (max-width: 768px) {
  .card {
    top: 33%;
    width: 350px;
    height: 500px;
    transform: translate(-50%);
    margin-bottom: 1rem;
  }
  .container {
    display: flex;
    justify-content: center;
    left: 50%;
    transform: translate(-55%);
    flex-direction: column;
    margin-bottom: 100px;
  }
} */

@media only screen and (max-width: 1232px) {
  .card {
    top: 70%;
    width: 300px;
    height: 450px;
    left: 45%;
    transform: translate(-50%, -50%);
    margin-bottom: 1rem;
  }
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-bottom: 100px;
  }
}

.item {
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 15%;
  border-radius: 10px;
  border-top: 3px solid #ffffff;
  border-right: 2px solid #ffff;
  border-bottom: 1px solid rgba(255, 255, 255, 0.364);
  border-left: 1px solid rgba(255, 255, 255, 0.364);

  z-index: 1;
}

@media only screen and (max-width: 768px) {
  .item {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    height: 50px;
    bottom: -10%;
    left: 50%;
    transform: translate(-50%);
    z-index: 1;
  }
}

@media only screen and (max-width: 992) {
  .item {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    height: 50px;
    bottom: -10%;
    left: 20%;
    z-index: 1;
  }
}

.bi-github,
.bi-linkedin,
.bi-window {
  transition: 0.5s ease-in-out;
  font-size: 30px;
  color: #7524ab83;

  text-shadow: 0mm 0mm 1mm rgba(11, 6, 6, 0.478);
  margin: 20px;
  cursor: pointer;
}

.bi-github:hover,
.bi-linkedin:hover,
.bi-window:hover {
  backdrop-filter: blur(1rem);
  transition: 0.3s ease-in-out;
  color: #ffffff;
}

.write {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  background: rgba(255, 255, 255, 0.089);
  width: 5rem;
  height: 5rem;
  bottom: 3.5%;
  right: 4.4%;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  box-shadow: 0mm 0mm 1mm white;
}
.write i {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  width: 5rem;
  height: 5rem;
  color: white;
}
.write:hover {
  cursor: pointer;
  transition: 0.3s ease-in-out;
  box-shadow: 0mm 0mm 1mm purple;
  background: rgb(255, 255, 255);
}

.bi-pen {
  font-size: 26px;
}
.bi-pen:hover {
  transition: 0.3s ease-in-out;
  color: purple;
}

.area {
  height: 400px;
  width: 350px;
  margin: 1.3rem;
  padding: 1rem;
  background: rgba(0, 0, 0, 0.093);
  backdrop-filter: blur(0.5rem);
  box-shadow: 0mm 0mm 1mm rgba(255, 255, 255, 0.52);
  border: none;
  border-radius: 30px;
  outline: none;
}
</style>
