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
    methods :{
        nextPage(){
            this.$emit('next-page');
        },
        prevPage(){
            this.$emit('prev-page');
        }
    }
};
</script>

<style scoped>
.pagination {
  font-size: 20px;
  font-weight: 300;
  display: flex;
  justify-content: flex-end;
}

.pagination li {
  text-align: center;
  display: inline-block;
  margin: 0 5px;
  width: 34px;
  height: 34px;
  border: 2px solid lightgray;
  border-radius: 3px;
}

.pagination li:hover {
  border: 2px solid rgb(62, 62, 253);
  color: rgb(62, 62, 253);
  cursor: pointer;
}
</style>