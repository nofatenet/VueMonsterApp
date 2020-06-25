<template>
  <header class="header">
    <div id="header">
      <h1 class="white-text bigText">{{ AppTitle }}</h1>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data: function() {
    return {
      AppTitle: "Vue Monster"
    };
  }
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 0px;
}

html {
  font-size: 14px;
}
.header {
  background: #333;
  color: #eee;
  padding: 12px;
  box-shadow: 0 4px 12px -3px rgba(60, 60, 60, 0.6);
  text-align: center;
}

.header a {
  color: #fff;
  padding-right: 6px;
}
</style>