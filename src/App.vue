<template>
  <div id="app">
    <h1 class="title">Mauke Dictionary</h1>
    <div class="list-wrap">
      <AlphabetList :list="list" />
    </div>
  </div>
</template>

<script>
import dictionary from "./dictionary.json";
import AlphabetList from "./components/AlphabetList";

export default {
  name: "App",
  components: {
    AlphabetList,
  },
  data() {
    return {
      list: dictionary.data,
    };
  },
};
</script>

<style lang="scss">
@import url("~reset-css/reset.css");

html,
body {
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

#app {
  width: 100%;
  height: 100%;
  padding: 20px 10px 0;
  box-sizing: border-box;
  overflow: auto;

  .title {
    font-size: 2em;
    font-weight: bold;
    margin-bottom: 10px;
    font-family: "SUSE", sans-serif;
    color: #004eaa;
  }

  .list-wrap {
    position: relative;
    width: 100%;
    height: calc(100% - 52px);
  }
}
</style>
