<template>
  <div id="app">
    <header>
      <h2>
        <span class="bold">GitHub</span> Jobs
      </h2>
    </header>
    <router-view />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Catamaran:wght@100;200;300;400;500;600;700;800;900&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  width: 75%;
  margin: auto;
  font-family: 'Catamaran', sans-serif;
  font-weight: 100;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #334680;
  background-color: #f6f7fb;
}

#app {
  text-align: center;
}

footer {
  text-align: center;
  margin: 60px;
}

header {
  text-align: left;
  padding: 10px;
  height: 50px;
  color: rgba(0, 0, 0, 0.801);
}

input[type="text"] {
  outline: none;
  font-size: 16px;
  padding-left: 10px;
  height: 40px;
}

li {
  list-style-type: none;
  text-align: left;
}

.shadow {
  box-shadow: 0 2px 1px 0 rgba(155, 155, 155, 0.2);
}

.bold{
  font-weight: 900;
}

::placeholder {
  color:rgb(150, 150, 150, .8);
  font-size: 14px;
}

@media only screen and (max-width: 600px) {
  body {
    width: 98%;
  }
}
</style>
