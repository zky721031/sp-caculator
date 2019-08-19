<template>
  <div id="app">
    <h6>{{ title }}</h6>
    <caculator></caculator>
  </div>
</template>

<script>
import caculator from "./components/caculator";

export default {
  name: "App",
  components: {
    caculator
  },
  data() {
    return {
      title: "hey my first caculator! just do it!"
    };
  }
};
</script>

<style>
html,
body {
  background-color: #333;
}
h6 {
  color: #fff;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  font-size: 2rem;
}
</style>
