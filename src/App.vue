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
}

body {
  width: 75%;
  margin: auto;
  font-family: 'Catamaran', sans-serif;
  font-weight: 100;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #243d57;
  background-color: #eee;
}

#app {
  text-align: center;
}

footer {
  text-align: center;
  margin: 10px;
}

header {
  text-align: left;
  padding: 20px;
  height: 30px;
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
</style>
