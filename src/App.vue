<template>
  <div id="app">
    <button v-if="isMain" class="main-btn" @click="isMain = false">
      Налоговый вычет
    </button>
    <Card v-else @close="isMain = true" />
  </div>
</template>

<script>
import Card from "./components/Card.vue";
export default {
  name: "App",
  data() {
    return {
      isMain: true,
    };
  },
  components: { Card },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  height: 100%;
}
body {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
      255.35deg,
      #dc3131 0.83%,
      rgba(255, 79, 79, 0) 108.93%
    ),
    #ff5e56;
  box-shadow: 0px -0.11px 16.9495px rgba(183, 187, 225, 0.33);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.main-btn {
  padding: 16px 32px;
  border: 1px solid white;
  background: inherit;
  color: white;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  margin: 0;
  box-shadow: (0px 0px 44px #cfdae7);
  border-radius: 6px;
  cursor: pointer;
} 


.main-btn:hover,
.main-btn:active {
  background-color: white;
  color: black;
  box-shadow: none;
}

.main-btn:disabled {
  background: #bec5cc;
}
</style>
