<template>
  <div id="app">
    <div id="nav">
      <router-link to="/imagebox"
        ><span style="color:red">Imagebox</span></router-link
      >
      |
      <router-link to="/webgallery"
        ><span style="color:red">Webgallerie</span></router-link
      >
    </div>
    <router-view />
  </div>
</template>
<script>
// @ is an alias to /src

export default {
  name: "app",
  components: {},
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /*color: #2c3e50;*/
  color: black;
  /* background-image: url("assets/image.gif"); */
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
/* my styles */

#container {
  display: flex;
  /* background-color: green;*/
  height: "1000px";
  flex-direction: column;
  justify-content: space-between;
  /* z-index: 20;*/
}
#imagebox {
  /*background-color: red;*/
  display: flex;
  flex-direction: row;
  justify-content: center;
  /* z-index: -1;*/
}
#images {
  /* background-color: blue;*/
  height: 300px;
  width: 50%;
}
#images img {
  width: 100%;
  height: 100%;
}
#buttonbox {
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
#textinputbox {
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
#textinputbox input {
  width: 50%;
}
#bottombuttonbox {
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
#pricetitlebox {
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
</style>
