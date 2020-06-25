<template>
  <div id="app">
    <Header />
    <VueMonsterApp />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import VueMonsterApp from "./components/VueMonsterApp.vue";

export default {
  name: "App",
  components: {
    VueMonsterApp,
    Header
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
}

html {
  font-size: 14px;
  background-color: #000;
}

html,
* {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Ubuntu,
    "Helvetica Neue", Helvetica, sans-serif;
  line-height: 1;
}

body {
  margin: 0px;
}

h1 {
  margin: 0;
  padding: 10px 25px;
  font-size: 1.5em;
  /* font-weight: bold; */
}

div.inner-box {
  margin: 20px;
}

.rounded {
  border-radius: 10px;
  -webkit-border-radius: 10px;
}

label {
  font-size: 1em;
}

.box-container {
  /* margin: 0 20px; */
  padding: 10px 10px 10px 10px;
  display: inline-block;
}

.white-text {
  color: #fff !important;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: 400;
  /* line-height: 1.3; */
}

.bigText {
  font-size: 2.4em;
}

[type="checkbox"] {
  top: 0;
  width: 20px;
  height: 20px;
  border: 2px solid #3f82b7;
  background-color: #3f82b7;
  z-index: 0;
  border-radius: 2px;
}

input:hover {
  background-color: #fff;
}

input,
label {
  margin: 4px;
  padding: 4px;
  display: flex;
  width: 90%;
}

#errorMessage {
  margin: 0em;
  padding: 0em;
  border-radius: 4px;
  color: #600;
  font-weight: bold;
}

.flex-container {
  display: flex;
  flex-flow: row;
  padding: 1px;
  margin: 0px;
  list-style: none;
}

.flex-item {
  background: #ddd;
  padding: 4px;
  width: 20em;
  margin: 4px;
  line-height: 30px;
  border-radius: 4px;
  text-align: center;
}
</style>
