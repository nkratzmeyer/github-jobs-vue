<template>
  <div>
    <ul class="pagination">
      <li v-on:click="prevPage">&lt;</li>
      <li v-on:click="nextPage">&gt;</li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    nextPage() {
      this.$emit("next-page");
    },
    prevPage() {
      this.$emit("prev-page");
    },
  },
};
</script>

<style scoped>
.pagination {
  font-size: 26px;
  font-weight: 300;
  display: flex;
  justify-content: flex-end;
}

.pagination li {
  text-align: center;
  display: inline-block;
  margin: 0 5px;
  width: 36px;
  height: 36px;
  border: 1px solid #b7bcce;
  border-radius: 4px;
  color: #b7bcce;
  line-height: 36px;
}

.pagination li:hover {
  border: 2px solid #1E86FF;
  color: #1E86FF;
  cursor: pointer;
}
</style>