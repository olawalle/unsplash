<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
@import "node_modules/bootstrap/scss/bootstrap";
@import "node_modules/bootstrap-vue/src/index.scss";
@import url("https://fonts.googleapis.com/css?family=Rubik&display=swap");
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 0;
  font-family: "Rubik", sans-serif;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.modal-body {
  padding: 0px !important;
  border-radius: 0px !important;
  overflow: hidden !important;
  ::-webkit-scrollbar {
    width: 5px;
  }
  ::-webkit-scrollbar-track {
    background: #f1f1f1;
  }
  ::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 15px;
  }
  ::-webkit-scrollbar-thumb:hover {
    background: #555;
  }
}
</style>
