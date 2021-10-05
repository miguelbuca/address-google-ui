<template>
  <!--<div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>-->
  <router-view/>
</template>

<style>
:root{
  --primary: #42b983;
  --sec: #2c3e50;
}
*,
::after,
::before{
  margin: 0;
  padding: 0;
}
html,
body{
  position: relative;
  display: flex;
  flex-direction: column;
  height: 100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  flex: 1;
  display: flex;
}
button,input,select{
  padding: .5rem 1rem;
  outline: none;
  border: solid 1px transparent;
  border-radius: 4px;
}
input,select{
  background-color: rgba(0, 0, 0, .06);
  transition: all .2s;
  color: var(--primary);
  min-width: 20rem;
}
input:focus-within,select:focus-within{
  border: solid 1px var(--primary);
}
button{
  background-color: var(--primary);
  color: #fff;
  cursor: pointer;
}
a,
a:link,
a:visited{
  outline: none;
  color: var(--primary);
  text-decoration: none;
  padding-bottom: .1rem;
  /*border-bottom: solid 1px var(--primary);*/
}
</style>
