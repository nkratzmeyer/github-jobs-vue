<template>
  <div class="search-area">
    <input v-model="searchTerm" type="text" 
    v-on:keyup.enter="handleSearchClick"
    placeholder="Title, company, expertise, or benefits"  />
    <button v-on:click="handleSearchClick">Search</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: "",
    };
  },
  methods: {
    handleSearchClick() {
      this.$emit("search", this.searchTerm);
      this.searchTerm = '';
    },
  },
};
</script>

<style scoped>
.search-area {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px auto 25px auto;
  padding: 5px;
  width: 100%;
  height: 90px;
  background-image: url("../assets/backgroundImg.png");
  text-align: left;
  border-radius: 10px;
}

.search-area input[type="text"] {
  width: 500px;
}

.search-area button {
  font-size: 18px;
  width: 100px;
  height: 44px;
  background-color: #4646ec;
  color: white;
  border: none;
  outline: none;
}

.search-area button:hover {
  background-color: blue;
  cursor: pointer;
}
</style>