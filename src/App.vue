<template>
  <div id="app">
    <audio autoplay="true" src="@/assets/mrs-fens-gaggles-mastered.wav"></audio>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/info">Info</router-link>
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
}



:root, body {
  background-image: url(~@/assets/BACKGROUND.png);
}

    @font-face { font-family: Monaco;
    src: url('~@/assets/monaco.ttf');}


.statsandother
{
  font-size: 20px;
  color: white; 
  background-color: rgba(100, 100, 100, 0.8);
  border-radius: 10px;
  padding: 10px;
  padding-top: 0px;
  margin-top: 30px;
  position:absolute;
  margin-left:190px;
}

.statsandotherselected
{
  font-size: 20px;
  color: white; 
  background-color: rgba(136, 0, 0, 0.8);
  border-radius: 10px;
  padding: 10px;
  padding-top: 0px;
  margin-top: 30px;
  position:absolute;
  margin-left:190px;
}

.credits {
  font-size: 20px;

}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: black ;
}

#nav a.router-link-exact-active {
  color: white;
}

main {
  max-width: 760px; margin: auto; 
}
</style>
