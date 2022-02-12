<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #c43c4e;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #d31525;
}

#nav a.router-link-exact-active {
  color: #d311a2;
}

main {
  max-width: 760px; margin: auto; 
}
</style>
