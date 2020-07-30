<template>
  <div id="app">
    <header>
      <h1 class="title">
        <span class="bold">GitHub</span> Jobs
      </h1>
    </header>
    <router-view />
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  width: 75%;
  margin: auto;
  font-family: Roboto, sans-serif;
  font-weight: 100;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #334680;
  background-color: #F6F7FB;
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

header .title{
font-family: Poppins;
font-style: normal;
font-weight: bold;
font-size: 24px;
line-height: 36px;
color: #282538;
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

/* Loader */
.loading {
  display: inline-block;
  width: 50%;
  height: 80px;
}
.loading::before {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: auto;
  border-radius: 50%;
  border: 6px solid rgb(255, 255, 255);
  border-color: rgb(53, 50, 253) transparent rgb(82, 107, 248) transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@media only screen and (max-width: 600px) {
  body {
    width: 98%;
  }
}
</style>
