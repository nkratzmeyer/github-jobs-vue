<template>
  <div class="search-box">
    <input type="text" placeholder="Title, company, expertise, or benefits" />
    <input type="text" placeholder="City, state, zipcode, or country" />
    <div>
      <input type="checkbox" name="full-time" />
      <label for="full-time">Full Time Only</label>
    </div>
    <button>Search</button>
  </div>
</template>

<style scoped>
.search-box {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px auto;
  padding: 5px;
  width: 100%;
  height: 50px;
  background-color: rgb(143, 139, 139);
  text-align: left;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.search-box input[type="text"] {
  margin-right: 15px;
  font-size: 16px;
  width: 400px;
  height: 30px;
  padding-left: 10px;
}

.search-box button {
  margin-left: 15px;
  font-size: 18px;
  width: 100px;
  height: 35px;
  background-color: #4646ec;

  color: white;
  border: 1px solid gray;
}

.search-box button:hover {
  background-color: blue;
  cursor: pointer;
}
</style>