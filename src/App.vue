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
  font-size: 30px;
  font-family: Monaco;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000; 
  text-shadow:
    -1px -1px 0 rgb(255, 255, 255),
    1px -1px 0 rgb(255, 255, 255),
    -1px 1px 0 rgb(255, 255, 255),
    1px 1px 0 rgb(255, 255, 255);  
}



:root, body {
  background-image: url(~@/assets/BACKGROUND.png);
}

    @font-face { font-family: Monaco;
    src: url('~@/assets/monaco.ttf');}

.strokeme
{
    text-shadow:
    -1px -1px 0 rgb(255, 255, 255),
    1px -1px 0 rgb(255, 255, 255),
    -1px 1px 0 rgb(255, 255, 255),
    1px 1px 0 rgb(255, 255, 255);  
}

.statsandother
{
  font-size: 20px;
  color: #2346a8; 
  text-shadow:
  -1px -1px 0 #c0f6ff,
  1px -1px 0 #c0f6ff,
  -1px 1px 0 #c0f6ff,
  1px 1px 0 #c0f6ff;
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
