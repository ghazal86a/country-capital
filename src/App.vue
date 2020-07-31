<template>
  <div id="app">
    <div id="nav">
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

html {
  width: 100%;
  height: 100%;
}

body {
  background: linear-gradient(45deg,  rgba(66, 245, 135, 0.8) 0%,rgba(66, 245, 189,0.4) 100%);
  color: rgba(#000000, 0.6);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
