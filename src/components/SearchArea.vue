<template>
  <div class="search-area">
    <div class="input-area">
      <i class="fa fa-search" aria-hidden="true"></i>
      <input
        v-model="searchTerm"
        type="text"
        v-on:keyup.enter="handleSearchClick"
        placeholder="Title, company, expertise, or benefits"
      />
      <button v-on:click="handleSearchClick">Search</button>
    </div>
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
      this.searchTerm = "";
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
  height: 100px;
  background-image: url("../assets/backgroundImg.png");
  border-radius: 10px;
}

.input-area {
  width: 790px;
  height: 50px;
  background: #ffffff;
  box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  padding-left: 10px;
}

.search-area input[type="text"] {
  width: 80%;
  height: 100%;
  border: none;
}

.search-area button {
  font-size: 18px;
  width: 18%;
  height: 86%;
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